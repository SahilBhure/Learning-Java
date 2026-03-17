
## 1. What is Spring Boot and how is it different from Spring Framework?

Spring Boot is an opinionated framework built on top of Spring that:

* Eliminates boilerplate configuration
* Provides auto-configuration
* Embeds servers (Tomcat, Jetty)

Key difference:

> Spring = framework
> Spring Boot = tool to simplify Spring setup and production readiness

---

## 2. What is Auto-Configuration in Spring Boot?

Auto-configuration automatically configures beans based on:

* Classpath dependencies
* Existing beans
* Application properties

---

### Internal Mechanism

* Uses `@EnableAutoConfiguration`
* Loads configuration from:

```text
META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports
```

---

## 3. How does Spring Boot decide which configuration to apply?

It uses:

* `@Conditional` annotations

Examples:

* `@ConditionalOnClass`
* `@ConditionalOnMissingBean`
* `@ConditionalOnProperty`

---

## 4. What is @SpringBootApplication?

Combination of:

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan
```

---

## 5. Explain Spring Boot Startup Flow (Deep)

1. `main()` method runs
2. `SpringApplication.run()`
3. Creates ApplicationContext
4. Loads auto-configurations
5. Scans components
6. Initializes beans
7. Starts embedded server

---

## 6. What is SpringApplication?

Core class that bootstraps application.

Handles:

* Environment setup
* Context creation
* Listeners and initializers

---

## 7. What are Starters in Spring Boot?

Predefined dependency bundles.

Example:

* `spring-boot-starter-web`
* `spring-boot-starter-data-jpa`

---

## 8. Why are Starters important?

* Avoid dependency conflicts
* Provide curated dependency sets
* Reduce manual configuration

---

## 9. What is Embedded Server?

Spring Boot includes:

* Tomcat (default)
* Jetty
* Undertow

---

### Benefit

> No need to deploy WAR file externally

---

## 10. How to change embedded server?

```xml
Exclude Tomcat, add Jetty
```

---

## 11. What is application.properties vs application.yml?

Both define configuration.

YAML:

* More readable
* Supports hierarchy

---

## 12. Configuration Loading Order (Very Important)

Priority:

1. Command line args
2. Environment variables
3. application.properties/yml
4. Defaults

---

## 13. What are Profiles?

Used for environment-specific configs.

---

### Example

```properties
spring.profiles.active=prod
```

---

## 14. What is Externalized Configuration?

Keeping configs outside code:

* Properties files
* Environment variables
* Config server

---

## 15. What is @ConfigurationProperties?

Binds properties to Java object.

---

### Example

```java
@ConfigurationProperties(prefix = "app")
class AppConfig {
}
```

---

## 16. Difference between @Value and @ConfigurationProperties?

* `@Value` → individual property
* `@ConfigurationProperties` → bulk binding

---

## 17. What is CommandLineRunner?

Runs code after application startup.

---

## 18. What is ApplicationRunner?

Similar to CommandLineRunner but provides structured arguments.

---

## 19. What is Spring Boot DevTools?

Provides:

* Auto restart
* Live reload
* Dev-time enhancements

---

## 20. What is Actuator?

Provides production endpoints for:

* Health
* Metrics
* Monitoring

---

## 21. How to secure Actuator?

Restrict endpoints via Spring Security.

---

## 22. What is Spring Boot CLI?

Command-line tool to run Spring apps quickly.

---

## 23. What is Fat Jar (Uber Jar)?

Single executable JAR with:

* App code
* Dependencies
* Embedded server

---

## 24. How does Spring Boot handle logging?

Uses:

* Logback (default)

---

## 25. What is Banner in Spring Boot?

Startup message.

---

### Disable

```properties
spring.main.banner-mode=off
```

---

## 26. What is Lazy Initialization?

Beans are created only when needed.

---

## 27. How to enable Lazy Initialization?

```properties
spring.main.lazy-initialization=true
```

---

## 28. What is Spring Boot Starter Parent?

Provides:

* Dependency management
* Plugin configuration

---

## 29. What is AutoConfigurationImportSelector?

Loads auto-config classes dynamically.

---

## 30. How to exclude auto-configuration?

```java
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
```

---

## 31. What is Spring Boot Loader?

Handles:

* Executing fat JAR
* Class loading

---

## 32. What is @EnableAutoConfiguration?

Triggers auto-configuration mechanism.

---

## 33. What is SpringFactoriesLoader?

Loads configuration from `spring.factories` (older mechanism).

---

## 34. What is difference between @ComponentScan and @EnableAutoConfiguration?

* ComponentScan → scans user-defined beans
* EnableAutoConfiguration → loads framework configs

---

## 35. What is ApplicationContext?

Spring container holding beans.

---

## 36. What is Environment in Spring Boot?

Provides access to:

* Properties
* Profiles

---

## 37. What is ConfigurableApplicationContext?

Extended ApplicationContext with lifecycle control.

---

## 38. What is Bean overriding?

Replacing existing bean definition.

---

## 39. What is @ConditionalOnMissingBean?

Loads bean only if none exists.

---

## 40. What is @ConditionalOnBean?

Loads bean only if another bean exists.

---

## 41. What is @ConditionalOnProperty?

Loads config based on property value.

---

## 42. What is WebServerFactoryCustomizer?

Customize embedded server.

---

## 43. What is Error Handling in Spring Boot?

Handled using:

* @ControllerAdvice
* ErrorController

---

## 44. What is Whitelabel Error Page?

Default error page.

---

## 45. How to disable it?

```properties
server.error.whitelabel.enabled=false
```

---

## 46. What is Spring Boot Packaging?

* JAR (default)
* WAR (for external server)

---

## 47. What is Spring Boot Test?

Provides testing utilities.

---

## 48. What is @SpringBootTest?

Loads full application context.

---

## 49. What is AutoConfigurationReport?

Debug auto-config decisions.

---

## 50. What is Spring Boot Admin?

UI for monitoring applications.

---

## 51. What is Graceful Shutdown?

Allows requests to complete before stopping.

---

## 52. What is Spring Boot Caching?

Supports:

* Redis
* EhCache

---

## 53. What is Configuration Metadata?

Helps IDE autocomplete properties.

---

## 54. What is @Import?

Imports additional configuration classes.

---

## 55. What is difference between run() and start()?

* `run()` → initializes context
* `start()` → lifecycle method

---

## 56. What are common pitfalls?

* Overusing auto-config
* Not understanding internals
* Poor config management

---

## 57. What is Spring Boot’s biggest advantage?

> Rapid development with production-ready defaults

---

## 58. What is its biggest drawback?

> Hidden complexity due to abstraction

---

## 59. When should you NOT use Spring Boot?

* Very small apps
* Memory-constrained environments

---

## 60. Final Advanced Insight

> Spring Boot is not magic — it is a structured system of:

* Conditional configuration
* Classpath scanning
* Bean lifecycle management

Understanding internals = mastering Spring Boot

---

