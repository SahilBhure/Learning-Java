
## Spring Configuration Deep Dive
---

## 2. What is Configuration in Spring?

Configuration = Metadata that tells Spring:

* Which classes to manage
* How to create beans
* How to wire dependencies

---

## 3. Types of Configuration

Spring supports 3 main configuration styles:

| Type               | Usage       | Status            |
| ------------------ | ----------- | ----------------- |
| XML Configuration  | Old style   | Rarely used       |
| Java Configuration | Modern      | Widely used       |
| Annotation-based   | Most common | Industry standard |

---

## 4. XML Configuration (Legacy)

Example:

```xml id="1yzv3o"
<beans>
    <bean id="engine" class="com.example.Engine"/>
    
    <bean id="car" class="com.example.Car">
        <property name="engine" ref="engine"/>
    </bean>
</beans>
```

Problems:

* Verbose
* Hard to maintain
* Not type-safe

---

## 5. Java-Based Configuration (Recommended)

### @Configuration

Marks a class as configuration:

```java id="6y7xw1"
@Configuration
public class AppConfig {
}
```

---

### @Bean

Defines a bean manually:

```java id="o3x2n9"
@Bean
public Engine engine() {
    return new Engine();
}
```

---

### Full Example

```java id="xj5q8p"
@Configuration
public class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine();
    }

    @Bean
    public Car car() {
        return new Car(engine());
    }
}
```

---

## 6. Annotation-Based Configuration (Most Used)

### @Component

```java id="h8k4rz"
@Component
public class Engine {
}
```

---

### Specialized Annotations

| Annotation  | Purpose        |
| ----------- | -------------- |
| @Component  | Generic bean   |
| @Service    | Business logic |
| @Repository | Database layer |
| @Controller | Web layer      |

---

## 7. Component Scanning

Spring automatically detects beans:

```java id="v6q3ka"
@Configuration
@ComponentScan("com.example")
public class AppConfig {
}
```

This scans the package and registers all annotated classes.

---

## 8. Combining Java Config + Annotations (Best Practice)

In real projects:

* Use `@Component` for most beans
* Use `@Bean` for external or complex objects

Example:

```java id="5w9p2d"
@Configuration
@ComponentScan("com.example")
public class AppConfig {

    @Bean
    public ObjectMapper objectMapper() {
        return new ObjectMapper();
    }
}
```

---

## 9. @Import (Modular Configuration)

```java id="p8c3zf"
@Configuration
@Import(DatabaseConfig.class)
public class AppConfig {
}
```

Used to:

* Split large configs
* Organize modules

---

## 10. @PropertySource (External Config)

```java id="0q2l7b"
@Configuration
@PropertySource("classpath:application.properties")
public class AppConfig {
}
```

Used with:

```java id="u1t9we"
@Value("${db.url}")
private String dbUrl;
```

---

## 11. Profiles (Environment-Based Config)

```java id="n3k8xa"
@Profile("dev")
@Bean
public DataSource devDataSource() {
    return new DevDataSource();
}
```

```java id="7r5ypl"
@Profile("prod")
@Bean
public DataSource prodDataSource() {
    return new ProdDataSource();
}
```

Run with:

```
-Dspring.profiles.active=dev
```

---

## 12. Configuration Best Practices

* Prefer **annotation-based config**
* Use `@Configuration` for setup
* Keep configs modular
* Avoid XML unless legacy project
* Use profiles for environments

---

## 13. Real-World Project Structure

```
com.example.project
│
├── config
│   ├── AppConfig.java
│   ├── DatabaseConfig.java
│
├── service
├── repository
├── controller
```

---

## 14. Common Mistakes

* Mixing all config styles randomly
* Overusing `@Bean` unnecessarily
* Not using profiles
* Large monolithic config classes

---
