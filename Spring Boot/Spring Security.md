
## Spring Security Deep Dive (Authentication, Authorization, JWT, Filters)

---

## 1. What is Spring Security (Deep Understanding)

Spring Security is not just a library for login/logout. It is a **comprehensive security framework** that sits in front of your application and controls **every incoming HTTP request**.

It works by:

* Intercepting requests before they reach controllers
* Authenticating users
* Authorizing access
* Managing security context per request

At its core, Spring Security is:

> **A filter-based security system integrated with Spring’s IoC container and AOP mechanisms**

---

## 2. High-Level Architecture (Internal Flow)

```text
Client Request
      ↓
Security Filter Chain
      ↓
Authentication Process
      ↓
SecurityContext (stored per request/thread)
      ↓
Authorization Check
      ↓
Controller → Service → DB
```

Important insight:

> Controllers are never reached unless the request passes through the entire security chain.

---

## 3. Security Filter Chain (Core Backbone)

### What it is

A sequence of filters where each filter:

* Performs a specific security task
* Passes request to next filter

Spring Security internally registers **dozens of filters**, such as:

* UsernamePasswordAuthenticationFilter
* BasicAuthenticationFilter
* SecurityContextPersistenceFilter
* ExceptionTranslationFilter

---

### How it works

1. Request enters application
2. First filter processes it
3. Passes to next filter
4. Continues until:

   * Authentication is done
   * Authorization is checked
   * Or request is rejected

---

### Custom Configuration

```java
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .anyRequest().authenticated()
        );
    return http.build();
}
```

---

### Key Insight

> The filter chain is the **real execution engine** of Spring Security.

Everything (JWT, login, roles) happens inside this chain.

---

## 4. Authentication (Deep Internal Flow)

Authentication answers:

> “Who is making this request?”

---

### Step-by-Step Internal Flow

1. Request hits authentication filter
2. Filter extracts credentials (username/password or token)
3. Creates an **Authentication object (unauthenticated)**
4. Passes it to AuthenticationManager
5. AuthenticationManager delegates to AuthenticationProvider
6. AuthenticationProvider:

   * Loads user via UserDetailsService
   * Verifies password using PasswordEncoder
7. If valid:

   * Returns authenticated Authentication object
8. Stored in SecurityContext

---

### Authentication Object

Represents:

* Principal (user)
* Credentials
* Authorities (roles)

---

## 5. AuthenticationManager (Core Coordinator)

### Role

Acts as a **central dispatcher** for authentication.

```java
Authentication authenticate(Authentication authentication);
```

---

### Internal Behavior

* Delegates authentication to multiple AuthenticationProviders
* Stops when one provider successfully authenticates

---

### Real Insight

> AuthenticationManager itself does not authenticate — it delegates.

---

## 6. AuthenticationProvider (Actual Auth Logic)

This is where real authentication happens.

---

### Responsibilities

* Validate credentials
* Load user details
* Compare password
* Return authenticated object

---

### Example

```java
public class CustomAuthProvider implements AuthenticationProvider {

    public Authentication authenticate(Authentication auth) {
        String username = auth.getName();
        String password = auth.getCredentials().toString();

        // validate user
        return new UsernamePasswordAuthenticationToken(username, password, List.of());
    }
}
```

---

### Key Insight

> You can plug in multiple providers:

* DB authentication
* LDAP
* OAuth
* Custom logic

---

## 7. UserDetailsService (User Loading Layer)

### Purpose

Loads user data from source (DB, API, etc.)

---

### Method

```java
UserDetails loadUserByUsername(String username);
```

---

### What UserDetails Contains

* Username
* Password (hashed)
* Roles/Authorities
* Account status (locked, expired, etc.)

---

### Important Insight

> This is NOT authentication — it only fetches user data.

---

## 8. PasswordEncoder (Security Critical)

### Why Needed

Passwords must NEVER be stored as plain text.

---

### BCrypt Example

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}
```

---

### Internal Behavior

* Adds random salt
* Hashes password
* Prevents rainbow table attacks

---

### Key Insight

> During login:

* Raw password → encoded → compared with stored hash

---

## 9. SecurityContext (Per Request Security Storage)

### What it stores

* Authentication object
* User identity
* Roles

---

### Access Example

```java
Authentication auth = SecurityContextHolder.getContext().getAuthentication();
```

---

### Internal Behavior

* Stored in ThreadLocal
* Cleared after request

---

### Key Insight

> This is how Spring knows “who is logged in” at any point.

---

## 10. Authorization (Access Control)

Authorization answers:

> “What is this user allowed to do?”

---

### URL-Based Authorization

```java
http
    .authorizeHttpRequests(auth -> auth
        .requestMatchers("/admin/**").hasRole("ADMIN")
        .requestMatchers("/user/**").hasAnyRole("USER", "ADMIN")
        .anyRequest().authenticated()
    );
```

---

### Method-Level Authorization

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser() {}
```

---

### Internal Flow

1. Request authenticated
2. Spring checks required roles
3. Compares with user authorities
4. Grants or denies access

---

## 11. Roles vs Authorities

### Role

* High-level concept
* Prefixed with `ROLE_`

### Authority

* Fine-grained permission

Example:

* ROLE_ADMIN → can have READ, WRITE, DELETE

---

## 12. CSRF Protection (Deep Understanding)

### Problem

CSRF attack:

* Malicious site sends request on behalf of user

---

### Solution

Spring Security:

* Generates CSRF token
* Validates token on request

---

### Why Disable for APIs?

```java
http.csrf().disable();
```

Because:

* APIs are stateless
* Use JWT instead of sessions

---

## 13. Stateful vs Stateless Security

### Stateful

* Uses HTTP session
* Server stores user data
* Default Spring Security behavior

---

### Stateless (Modern APIs)

* No session
* Each request carries authentication
* Typically uses JWT

---

### Key Insight

> Stateless systems scale better in distributed environments

---

## 14. JWT (Deep Dive)

### What is JWT?

A self-contained token that carries:

* User identity
* Roles
* Expiry

---

### Structure

```text
Header.Payload.Signature
```

---

### Example

Payload:

```json
{
  "sub": "user",
  "roles": ["USER"],
  "exp": 1712345678
}
```

---

### Signature

Ensures:

* Token is not tampered

---

## 15. JWT Authentication Flow

1. User logs in
2. Server validates credentials
3. Server generates JWT
4. Client stores token
5. Client sends token in header:
   Authorization: Bearer <token>
6. Server validates token on each request

---

## 16. JWT Filter (Critical Component)

### Purpose

Intercept every request to:

* Extract JWT
* Validate token
* Set authentication

---

### Example

```java
public class JwtFilter extends OncePerRequestFilter {

    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain chain) {

        String token = extractToken(request);

        if (validate(token)) {
            Authentication auth = createAuthentication(token);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }

        chain.doFilter(request, response);
    }
}
```

---

### Key Insight

> This filter replaces session-based authentication in stateless systems

---

## 17. Adding JWT Filter to Chain

```java
http.addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class);
```

---

### Why Before?

Because:

* JWT must be validated before authentication logic runs

---

## 18. Exception Handling in Security

Two main handlers:

### AuthenticationEntryPoint

* Handles unauthenticated access

### AccessDeniedHandler

* Handles unauthorized access

---

## 19. Security Configuration (Modern Style)

```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

    http
        .csrf(csrf -> csrf.disable())
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/auth/**").permitAll()
            .anyRequest().authenticated()
        );

    return http.build();
}
```

---

## 20. Internal Design Insight

Spring Security combines:

* **Filters (Servlet layer)**
* **AOP (method security)**
* **IoC container (bean management)**

---

## 21. Critical Pitfalls (Deep Understanding)

* Self-invocation bypasses method security
* Wrong filter order breaks authentication
* Stateless systems without proper token validation are insecure
* Misconfigured roles lead to privilege escalation

---

## 22. Real-World Architecture

```text
Client
  ↓
JWT Token
  ↓
Security Filter Chain
  ↓
JWT Filter
  ↓
SecurityContext
  ↓
Authorization
  ↓
Controller
```
