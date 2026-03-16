# Service-to-Service Communication

In a microservices architecture, services often need to communicate with each other.
For example, an **Order Service** might need to fetch user details from a **User Service**.

In this step, we will learn how one microservice can call another microservice using HTTP.

We will use:

* REST-based communication
* Spring's `RestTemplate`

---

# What You Will Learn

In this step you will learn:

* How microservices communicate with each other
* How to call another service using HTTP
* How to use `RestTemplate`
* How to integrate external API calls into a service layer

---

# Example Architecture

Consider two microservices.

```
User Service
Provides user data

Order Service
Requests user data
```

The communication flow looks like this:

```
Client
   |
Order Service
   |
HTTP Request
   |
User Service
```

The Order Service sends a request like:

```
GET http://localhost:8080/users/1
```

The User Service returns the user data.

---

# Add RestTemplate Bean

To make HTTP requests in Spring Boot, we need a `RestTemplate` bean.

Create a configuration class.

File:

```
src/main/java/com/example/helloservice/config/AppConfig.java
```

```java
package com.example.helloservice.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

@Configuration
public class AppConfig {

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

This allows Spring to inject `RestTemplate` wherever it is needed.

---

# Create a DTO for External Data

When calling another microservice, we usually map the response to a DTO.

Create a package:

```
dto
```

Create the file:

```
UserDTO.java
```

```java
package com.example.helloservice.dto;

public class UserDTO {

    private Long id;
    private String name;
    private String email;

    public UserDTO() {}

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

This class represents the response returned from another service.

---

# Update the Service Layer

We will update the service layer so it can call another microservice.

File:

```
src/main/java/com/example/helloservice/service/UserService.java
```

```java
package com.example.helloservice.service;

import com.example.helloservice.dto.UserDTO;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class UserService {

    private final RestTemplate restTemplate;

    public UserService(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    public UserDTO getUserFromUserService(Long id) {

        String url = "http://localhost:8080/users/" + id;

        return restTemplate.getForObject(url, UserDTO.class);
    }
}
```

Explanation:

| Component      | Purpose                                    |
| -------------- | ------------------------------------------ |
| RestTemplate   | Makes HTTP requests                        |
| getForObject() | Sends GET request and maps response to DTO |

---

# Create a Controller Endpoint

Create an endpoint to trigger the external service call.

File:

```
src/main/java/com/example/helloservice/controller/UserController.java
```

Add the following method:

```java
@GetMapping("/external/{id}")
public UserDTO getExternalUser(@PathVariable Long id) {
    return userService.getUserFromUserService(id);
}
```

This endpoint calls another service and returns the response.

---

# Run the Services

To test service communication:

1. Start the **User Service** on port `8080`.

2. Start another service that calls it.

---

# Test the API

Send a request:

```
GET http://localhost:8080/users/external/1
```

The service will internally call:

```
GET http://localhost:8080/users/1
```

Response example:

```json
{
  "id": 1,
  "name": "Sahil",
  "email": "sahil@example.com"
}
```

---

# How Microservices Communicate

Common communication methods include:

| Method    | Description                             |
| --------- | --------------------------------------- |
| REST      | HTTP-based communication                |
| gRPC      | High-performance RPC protocol           |
| Messaging | Asynchronous communication using queues |

REST communication is the most commonly used approach for simple microservices.

---

# Result

You now understand how one microservice can call another using HTTP.

This introduces an important concept in microservice architectures:
**service-to-service communication**.

The application now demonstrates how to:

* Make HTTP requests from one service to another
* Use RestTemplate in Spring Boot
* Map external responses to DTO objects
