

## 1. Explain Inversion of Control (IoC) in Spring beyond definition. How does it improve architecture?

IoC is not just about “Spring creating objects.” It fundamentally changes how systems are designed by **decoupling object creation from business logic**.

In traditional systems:

* Classes are tightly coupled because they instantiate dependencies directly.
* This leads to rigid architecture and difficult testing.

With IoC:

* Object creation is delegated to the container.
* Dependencies are injected at runtime.
* This enables **loose coupling, better modularity, and easier testing**.

Internally, Spring achieves this using:

* Bean definitions
* Reflection
* Dependency resolution algorithms

---

## 2. How does Dependency Injection work internally in Spring?

Spring DI works in multiple phases:

1. **Bean Definition Loading**

   * Reads metadata from annotations/XML/Java config

2. **Bean Creation**

   * Uses reflection to instantiate objects

3. **Dependency Resolution**

   * Matches dependencies by type, qualifier, or name

4. **Injection**

   * Constructor, setter, or field injection

5. **Post-processing**

   * BeanPostProcessors modify beans if needed

Spring uses:

* `DefaultListableBeanFactory`
* Reflection APIs
* Caching for singleton beans

---

## 3. Why is constructor injection preferred over field injection in production systems?

Constructor injection enforces:

* **Immutability** → dependencies cannot change
* **Mandatory dependencies** → prevents null issues
* **Testability** → easy to mock dependencies

Field injection:

* Breaks encapsulation
* Hard to unit test
* Not suitable for large-scale systems

---

## 4. Explain Bean Lifecycle in detail with internal hooks.

Lifecycle steps:

1. Instantiation
2. Dependency Injection
3. Aware interfaces (`BeanNameAware`, etc.)
4. `BeanPostProcessor#beforeInitialization`
5. `@PostConstruct`
6. `afterPropertiesSet()`
7. Custom init methods
8. `BeanPostProcessor#afterInitialization`
9. Bean ready

Destruction:

* `@PreDestroy`
* `DisposableBean.destroy()`

Important:
Spring heavily relies on **BeanPostProcessor** to implement features like AOP and transactions.

---

## 5. What is BeanPostProcessor and why is it powerful?

BeanPostProcessor allows:

* Intercepting bean creation
* Modifying beans dynamically

Used internally by Spring for:

* AOP proxies
* Security
* Transaction management

It is a key extension point in Spring.

---

## 6. Explain the difference between BeanFactory and ApplicationContext in depth.

BeanFactory:

* Lazy initialization
* Minimal features

ApplicationContext:

* Eager initialization
* Event system
* AOP integration
* Internationalization

In real-world apps:

> ApplicationContext is always used

---

## 7. How does Spring resolve dependency conflicts when multiple beans exist?

Resolution order:

1. By type
2. `@Qualifier`
3. `@Primary`
4. Bean name

If unresolved:

* Throws `NoUniqueBeanDefinitionException`

---

## 8. What are circular dependencies and how does Spring handle them?

Circular dependency:
A → B → A

Spring can resolve:

* **Setter injection cycles**

But fails for:

* Constructor injection cycles

Solution:

* Redesign architecture (best)
* Use `@Lazy` (temporary fix)

---

## 9. Explain Spring AOP proxy mechanism in depth.

Spring uses **proxy-based AOP**:

Types:

* JDK Dynamic Proxy (interfaces)
* CGLIB Proxy (classes)

Flow:

1. Bean is created
2. Wrapped in proxy
3. Method calls go through proxy
4. Advice applied

Limitation:

* Self-invocation bypasses proxy

---

## 10. Why does Spring AOP fail for self-invocation?

Because:

* Internal method calls do not go through proxy
* Proxy only intercepts external calls

Solution:

* Refactor logic into separate bean

---

## 11. Explain @Transactional internally.

@Transactional uses:

* AOP proxy
* PlatformTransactionManager

Flow:

1. Proxy intercepts method
2. Transaction begins
3. Method executes
4. Commit or rollback

---

## 12. Why does @Transactional not work on private methods?

Because:

* Spring AOP works via proxies
* Private methods cannot be overridden

Hence:

> Only public methods are proxied

---

## 13. Explain transaction propagation with real scenarios.

* REQUIRED → joins existing transaction
* REQUIRES_NEW → suspends old, creates new
* SUPPORTS → optional transaction

Use case:

* Logging service → REQUIRES_NEW
* Business logic → REQUIRED

---

## 14. What is the difference between JPA and Hibernate?

JPA:

* Specification

Hibernate:

* Implementation

Spring uses JPA abstraction to allow flexibility.

---

## 15. How does Spring Data JPA reduce boilerplate code?

* Generates queries from method names
* Provides default CRUD operations
* Uses proxies to implement repositories

---

## 16. Explain Lazy Loading vs Eager Loading.

Lazy:

* Loads data when needed
* Better performance

Eager:

* Loads immediately
* Can cause performance issues

---

## 17. What is N+1 problem?

Occurs when:

* One query fetches parent
* Multiple queries fetch children

Solution:

* Fetch joins
* Entity graphs

---

## 18. Explain Spring MVC request flow internally.

1. Request → DispatcherServlet
2. HandlerMapping finds controller
3. HandlerAdapter invokes method
4. ViewResolver resolves response

---

## 19. What is DispatcherServlet?

Front controller of Spring MVC:

* Handles all requests
* Routes them to controllers

---

## 20. How does Spring convert JSON to Java objects?

Using:

* Jackson ObjectMapper

Annotations:

* @RequestBody
* @ResponseBody

---

## 21. Why should we use DTOs instead of entities?

* Prevents data leakage
* Improves API flexibility
* Avoids exposing DB structure

---

## 22. What is @ControllerAdvice and why is it important?

Global exception handler:

* Centralized error handling
* Cleaner controllers

---

## 23. How does Spring handle validation internally?

Uses:

* Hibernate Validator
* JSR-380 (Bean Validation API)

---

## 24. Explain @ComponentScan in detail.

* Scans packages for beans
* Registers them in container

Uses:

* Classpath scanning
* Reflection

---

## 25. What are Spring Profiles and why are they important?

Profiles allow:

* Environment-based configuration

Example:

* dev vs prod DB configs

---

## 26. Explain how Spring manages singleton beans internally.

* Stores in cache (singleton registry)
* Returns same instance every time

---

## 27. What happens if prototype bean is injected into singleton?

* Only one instance created

Solution:

* Use ObjectFactory / Provider

---

## 28. Explain @Lazy annotation.

* Delays bean creation
* Useful for performance & circular dependencies

---

## 29. What is the role of ApplicationContextAware?

Allows bean to access:

* Spring container
* Other beans dynamically

---

## 30. How does Spring handle exception translation?

@Repository:

* Converts checked exceptions into runtime exceptions

---

## 31. What is the difference between checked and unchecked exceptions in Spring transactions?

* Runtime → rollback
* Checked → no rollback (default)

---

## 32. Explain the Open Session in View problem.

* Keeps session open for lazy loading
* Can cause performance issues

---

## 33. What is the role of HandlerInterceptor?

* Intercepts requests before/after controller

Used for:

* Logging
* Authentication

---

## 34. What is the difference between Filter and Interceptor?

Filter:

* Servlet level

Interceptor:

* Spring MVC level

---

## 35. Explain how Spring Boot simplifies Spring (conceptually).

* Auto-configuration
* Embedded server
* Starter dependencies

---

## 36. What are common performance issues in Spring apps?

* N+1 queries
* Over-fetching data
* Blocking operations

---

## 37. How does Spring manage thread safety in singleton beans?

* Beans must be stateless
* Spring does not enforce thread safety

---

## 38. What is the difference between @Bean and @Component?

@Bean:

* Manual configuration

@Component:

* Auto-detected

---

## 39. Explain the role of ProxyFactory in Spring.

* Creates AOP proxies
* Used internally by framework

---

## 40. What is the difference between compile-time and runtime weaving?

Spring uses:

* Runtime weaving (proxy-based)

AspectJ supports:

* Compile-time weaving

---

## 41. What is Dependency Resolution in Spring?

Process of:

* Matching dependencies
* Injecting correct beans

---

## 42. How does Spring handle bean initialization order?

* Depends on dependency graph
* Can use @DependsOn

---

## 43. What is the role of Environment abstraction?

Provides access to:

* Properties
* Profiles

---

## 44. What is @Value and how does it work?

Injects:

* Properties from config files

---

## 45. What is the difference between @RestController and @Controller in depth?

@RestController:

* Returns JSON directly

@Controller:

* Returns views

---

## 46. What are common pitfalls in Spring AOP?

* Self-invocation
* Wrong pointcuts
* Proxy limitations

---

## 47. How does Spring handle bean destruction?

* @PreDestroy
* DisposableBean
* Shutdown hooks

---

## 48. What is the difference between eager and lazy initialization?

Eager:

* Created at startup

Lazy:

* Created when needed

---

## 49. What is Dependency Lookup vs Dependency Injection?

Lookup:

* Bean fetched manually

Injection:

* Bean injected automatically

---

## 50. What are best practices for designing Spring applications?

* Layered architecture
* Constructor injection
* Use DTOs
* Keep beans stateless
* Proper exception handling

---

