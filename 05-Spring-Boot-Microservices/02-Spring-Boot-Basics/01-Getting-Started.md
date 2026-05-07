# Spring Boot Getting Started

## Table of Contents
1. [What is Spring Boot?](#what-is-spring-boot)
2. [Why Spring Boot?](#why-spring-boot)
3. [Project Setup](#project-setup)
4. [First Application](#first-application)
5. [Application Properties](#application-properties)

---

## What is Spring Boot?

Spring Boot is a framework built on top of Spring Framework that simplifies creating production-ready applications.

### Key Differences from Spring

| Feature | Spring | Spring Boot |
|---------|--------|-------------|
| Configuration | XML/Java | Auto-configuration |
| Boilerplate | High | Minimal |
| Embedded Server | No | Yes (Tomcat) |
| Dependency Management | Manual | Starters |
| Development | Slower | Faster |
| Production Ready | Manual setup | Out-of-box |

---

## Why Spring Boot?

### Problems Spring Boot Solves

1. **Configuration Hell**
   - Spring required extensive XML configuration
   - Spring Boot uses auto-configuration

2. **Dependency Management**
   - Spring required manual dependency versions
   - Spring Boot provides starter POMs

3. **Server Setup**
   - Spring required deploying to external server
   - Spring Boot has embedded Tomcat/Jetty

4. **Development Speed**
   - Spring projects had slow setup
   - Spring Boot allows quick start

---

## Project Setup

### Method 1: Spring Initializr (Recommended)

1. Visit https://start.spring.io/
2. Configure project:
   - **Project:** Maven Project
   - **Language:** Java
   - **Spring Boot:** Latest (e.g., 3.1.0)
   - **Packaging:** Jar
   - **Java Version:** 11+
3. Select dependencies:
   - Spring Web
   - Spring Data JPA
   - H2 Database
4. Click Generate
5. Extract and open in IDE

### Method 2: Command Line

```bash
# Install Spring Boot CLI
# https://spring.io/projects/spring-boot

# Create project
spring boot new --from=web my-app
cd my-app
```

### Method 3: IDE

**IntelliJ IDEA:**
- File → New → Project
- Select Spring Initializr
- Follow wizard

**Eclipse:**
- File → New → Other
- Search "Spring Starter"

---

## First Application

### Project Structure

```
my-app/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/
│   │   │       ├── Application.java
│   │   │       ├── controller/
│   │   │       ├── service/
│   │   │       ├── repository/
│   │   │       └── model/
│   │   └── resources/
│   │       ├── application.properties
│   │       └── application.yml
│   └── test/
├── pom.xml
└── README.md
```

### Main Application Class

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication  // Enables auto-configuration
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

### Create a Simple REST Endpoint

```java
package com.example.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    
    @GetMapping("/")
    public String hello() {
        return "Hello, Spring Boot!";
    }
    
    @GetMapping("/greet/{name}")
    public String greet(@PathVariable String name) {
        return "Hello, " + name + "!";
    }
}
```

### Run Application

```bash
# Using Maven
mvn spring-boot:run

# Using IDE
# Right-click Application.java → Run

# Access endpoints
# http://localhost:8080/
# http://localhost:8080/greet/John
```

---

## Application Properties

### application.properties

```properties
# Server Configuration
server.port=8080
server.servlet.context-path=/api

# Database
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# Logging
logging.level.root=INFO
logging.level.com.example=DEBUG

# Application Name
spring.application.name=My App
```

### application.yml

```yaml
server:
  port: 8080
  servlet:
    context-path: /api

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password
    driver-class-name: com.mysql.cj.jdbc.Driver
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect
  application:
    name: My App

logging:
  level:
    root: INFO
    com.example: DEBUG
```

### Environment-Specific Configuration

```
application.properties          (Default)
application-dev.properties      (Development)
application-prod.properties     (Production)
application-test.properties     (Testing)
```

Activate profile:
```properties
spring.profiles.active=dev
```

---

## Spring Boot Starters

Starters are dependency descriptors that simplify Maven/Gradle configuration.

### Common Starters

```xml
<!-- Web Development -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<!-- Data Access -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<!-- Database -->
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

<!-- Security -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<!-- Testing -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

---

## Running Tests

```java
import org.springframework.boot.test.context.SpringBootTest;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest
class ApplicationTests {
    
    @Test
    void contextLoads() {
        // Test passes if application context loads
    }
}
```

Run tests:
```bash
mvn test
```

---

## Interview Questions

### Q1: What is Spring Boot?
**Answer:** Spring Boot is a framework that simplifies creating Spring applications with minimal configuration, auto-configuration, and embedded servers.

### Q2: What does @SpringBootApplication do?
**Answer:** It enables auto-configuration, component scanning, and property configuration in one annotation.

### Q3: What are Spring Boot Starters?
**Answer:** Dependency descriptors that simplify Maven/Gradle configuration by bundling related dependencies.

### Q4: How to change the default port?
**Answer:** In application.properties: `server.port=8090`

### Q5: What's the difference between @Component and @RestController?
**Answer:** @Component is generic, @RestController is specialized for REST endpoints returning JSON.
