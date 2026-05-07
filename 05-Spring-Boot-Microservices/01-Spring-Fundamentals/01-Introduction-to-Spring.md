# Introduction to Spring Framework

## Table of Contents
1. [What is Spring?](#what-is-spring)
2. [Spring Architecture](#spring-architecture)
3. [Inversion of Control (IoC)](#inversion-of-control-ioc)
4. [Dependency Injection (DI)](#dependency-injection-di)
5. [Spring Modules](#spring-modules)
6. [Getting Started](#getting-started)

---

## What is Spring?

Spring is a lightweight, open-source Java framework for building enterprise applications. It simplifies Java development by providing:

- **Inversion of Control (IoC)** - Object management
- **Dependency Injection (DI)** - Loose coupling
- **Aspect-Oriented Programming (AOP)** - Cross-cutting concerns
- **Transaction Management** - Database operations
- **Web Framework** - MVC, REST APIs
- **Security** - Authentication, Authorization

### Benefits
- Reduces boilerplate code
- Improves testability
- Supports multiple Java technologies
- Large community support
- Production-ready

---

## Spring Architecture

### Core Modules

```
Spring Framework
├── Core Container
│   ├── Beans
│   ├── Core
│   ├── Context
│   └── SpEL (Expression Language)
├── Data Access
│   ├── JDBC
│   ├── ORM
│   ├── OXM
│   └── JMS
├── Web
│   ├── Servlet
│   ├── WebSocket
│   └── Portlet
├── AOP
└── Instrumentation
```

---

## Inversion of Control (IoC)

IoC is a design principle where object creation and management is delegated to a container.

### Without IoC (Tight Coupling)
```java
public class UserService {
    private UserRepository repository;  // Direct dependency
    
    public UserService() {
        this.repository = new UserRepository();  // Creating object
    }
}

// Problem: Hard to change implementation, hard to test
```

### With IoC (Loose Coupling)
```java
public class UserService {
    private UserRepository repository;
    
    // Spring injects the dependency
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}

// Spring handles object creation
```

### IoC Container
The Spring IoC Container manages:
- Object creation (Beans)
- Dependency injection
- Object lifecycle
- Bean configuration

---

## Dependency Injection (DI)

DI is a mechanism to inject dependencies into a class.

### Types of Dependency Injection

#### 1. Constructor Injection
```java
@Component
public class UserService {
    private UserRepository repository;
    
    // Constructor injection
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}
```

#### 2. Setter Injection
```java
@Component
public class UserService {
    private UserRepository repository;
    
    // Setter injection
    @Autowired
    public void setRepository(UserRepository repository) {
        this.repository = repository;
    }
}
```

#### 3. Field Injection
```java
@Component
public class UserService {
    @Autowired  // Field injection
    private UserRepository repository;
}
```

### Best Practice: Constructor Injection
```java
@Service
public class UserService {
    private final UserRepository repository;
    
    // Preferred: Constructor injection
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
    
    public User getUserById(Long id) {
        return repository.findById(id).orElse(null);
    }
}
```

---

## Spring Modules

### Spring Core
Core IoC container functionality.

```java
@Configuration
public class AppConfig {
    @Bean
    public UserRepository userRepository() {
        return new UserRepository();
    }
}
```

### Spring Context
Builds on Core module, provides advanced features.

```java
public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        UserService service = context.getBean(UserService.class);
    }
}
```

### Spring Beans
Manages bean lifecycle and configuration.

```java
@Component      // Generic component
@Service        // Business logic
@Repository     // Data access
@Controller     // Web layer
@Configuration  // Configuration class
public class MyClass {
    // ...
}
```

### Spring AOP
Provides aspect-oriented programming.

```java
@Aspect
@Component
public class LoggingAspect {
    @Before("execution(* com.example..*(..))")  // Pointcut
    public void logBefore(JoinPoint jp) {
        System.out.println("Method: " + jp.getSignature().getName());
    }
}
```

---

## Getting Started

### Project Setup with Spring Boot

#### 1. Create Project using Spring Initializr
```bash
# Visit https://start.spring.io/
# Select:
# - Project: Maven Project
# - Language: Java
# - Spring Boot: Latest version
# - Dependencies: Spring Web, Spring Data JPA
```

#### 2. Project Structure
```
src/
├── main/
│   ├── java/
│   │   └── com/example/
│   │       ├── Application.java
│   │       ├── controller/
│   │       ├── service/
│   │       ├── repository/
│   │       └── model/
│   └── resources/
│       ├── application.properties
│       └── application.yml
└── test/
```

#### 3. Simple Spring Application
```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}

// Model
@Entity
@Data
@NoArgsConstructor
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    private String email;
}

// Repository
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}

// Service
@Service
public class UserService {
    private final UserRepository repository;
    
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
    
    public User getUserById(Long id) {
        return repository.findById(id).orElse(null);
    }
}

// Controller
@RestController
@RequestMapping("/api/users")
public class UserController {
    private final UserService service;
    
    public UserController(UserService service) {
        this.service = service;
    }
    
    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return service.getUserById(id);
    }
}
```

---

## Bean Lifecycle

```
1. Instantiation
   ↓
2. Dependency Injection
   ↓
3. setBeanName() - if implements BeanNameAware
   ↓
4. setBeanFactory() - if implements BeanFactoryAware
   ↓
5. setApplicationContext() - if implements ApplicationContextAware
   ↓
6. @PostConstruct or afterPropertiesSet()
   ↓
7. Bean Ready to Use
   ↓
8. @PreDestroy or destroy()
```

### Example
```java
@Component
public class MyBean implements InitializingBean, DisposableBean {
    
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
    }
    
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("Properties set");
    }
    
    @PreDestroy
    public void destroy() {
        System.out.println("Bean destroyed");
    }
}
```

---

## Interview Questions

### Q1: What is Spring Framework?
**Answer:** Spring is a lightweight Java framework for building enterprise applications, providing IoC, DI, AOP, and other features.

### Q2: What's the difference between IoC and DI?
**Answer:** IoC is a design principle (framework controls object creation), DI is a mechanism to implement IoC (injecting dependencies).

### Q3: What are the types of Dependency Injection?
**Answer:** Constructor Injection, Setter Injection, and Field Injection. Constructor injection is preferred.

### Q4: What's a Bean in Spring?
**Answer:** A Bean is an object instantiated, assembled, and managed by the Spring IoC Container.

### Q5: Explain @Component, @Service, and @Repository?
**Answer:** Stereotypes for different layers. @Component is generic, @Service for business logic, @Repository for data access.
