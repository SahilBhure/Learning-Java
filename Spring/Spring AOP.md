
## Spring AOP (Aspect-Oriented Programming)
---

## 2. What is AOP?

**Aspect-Oriented Programming (AOP)** is a programming paradigm that:

> Separates cross-cutting concerns from business logic

---

## 3. What are Cross-Cutting Concerns?

These are functionalities used across multiple parts of an application:

* Logging
* Security
* Transactions
* Caching
* Monitoring

Problem without AOP:

```java
public void transferMoney() {
    log();
    checkSecurity();
    performTransaction();
    log();
}
```

Code becomes:

* Repetitive
* Hard to maintain

---

## 4. AOP Solution

AOP allows you to:

> Apply these concerns **without modifying business code**

---

## 5. Core AOP Concepts

### 5.1 Aspect

A class that contains cross-cutting logic

```java id="3d9x7k"
@Aspect
@Component
public class LoggingAspect {
}
```

---

### 5.2 Join Point

A point in execution:

* Method call
* Exception
* Field access

---

### 5.3 Advice

Action taken at a join point

Types:

* Before
* After
* After Returning
* After Throwing
* Around

---

### 5.4 Pointcut

Expression that selects join points

```java id="v9k2ap"
@Pointcut("execution(* com.example.service.*.*(..))")
public void serviceMethods() {}
```

---

### 5.5 Weaving

Process of applying aspects to target objects

Types:

* Compile-time
* Load-time
* Runtime (Spring uses this)

---

## 6. Types of Advice

### 6.1 Before Advice

```java id="2h7l5q"
@Before("execution(* com.example.service.*.*(..))")
public void beforeMethod() {
    System.out.println("Before method execution");
}
```

---

### 6.2 After Advice

```java id="6k3m1v"
@After("execution(* com.example.service.*.*(..))")
public void afterMethod() {
    System.out.println("After method execution");
}
```

---

### 6.3 After Returning

```java id="8x5q2z"
@AfterReturning("execution(* com.example.service.*.*(..))")
public void afterReturning() {
    System.out.println("Method returned successfully");
}
```

---

### 6.4 After Throwing

```java id="4c1t8n"
@AfterThrowing("execution(* com.example.service.*.*(..))")
public void afterException() {
    System.out.println("Exception occurred");
}
```

---

### 6.5 Around (Most Powerful)

```java id="7n2v9k"
@Around("execution(* com.example.service.*.*(..))")
public Object aroundMethod(ProceedingJoinPoint joinPoint) throws Throwable {
    System.out.println("Before");
    Object result = joinPoint.proceed();
    System.out.println("After");
    return result;
}
```

---

## 7. How Spring AOP Works Internally

Spring uses:

> **Proxies**

Types:

* JDK Dynamic Proxy (interfaces)
* CGLIB Proxy (classes)

Flow:

1. Bean is created
2. Spring wraps it in a proxy
3. Calls go through proxy
4. Advice is applied

---

## 8. Example: Logging Aspect

```java id="1p9x3v"
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore() {
        System.out.println("Logging before method");
    }
}
```

---

## 9. Enable AOP in Spring

```java id="0z8q2n"
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {
}
```

---

## 10. Real-World Use Cases

### Logging

* Automatically log method calls

### Security

* Check user roles

### Transactions

```java
@Transactional
public void transferMoney() {}
```

### Performance Monitoring

* Measure execution time

---

## 11. Pointcut Expressions (Important)

Syntax:

```id="7x2m1b"
execution(modifiers return-type package.class.method(args))
```

Example:

```java id="9m4k2c"
execution(* com.example.service.*.*(..))
```

Meaning:

* Any method
* Any return type
* Inside service package

---

## 12. Common Mistakes

* Wrong pointcut expressions
* Applying AOP to private methods (won’t work)
* Forgetting proxy limitations
* Overusing AOP

---

## 13. Limitations of Spring AOP

* Works only with method execution
* Proxy-based (not full AOP like AspectJ)
* Self-invocation problem

---

## 14. Best Practices

* Use AOP for cross-cutting concerns only
* Keep aspects simple
* Avoid business logic in aspects
* Prefer `@Around` for flexibility


