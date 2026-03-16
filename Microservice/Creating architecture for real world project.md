# Now lets try creating some architecture to understand how things works in Real Life Projects.

```
Controller  →  Service  →  Repository  →  Database
```

This separation keeps code clean, maintainable, and scalable.

---

# What We Will Learn

In this step you will learn:

* Layered architecture in Spring Boot
* Controller layer
* Service layer
* Repository layer
* Entity creation
* Basic CRUD structure

---

# Final Project Structure

Your project will look like this:

```
src/main/java/com/example/helloservice

├── controller
│     └── UserController.java
│
├── service
│     └── UserService.java
│
├── repository
│     └── UserRepository.java
│
├── model
│     └── User.java
│
└── HelloServiceApplication.java
```

Each layer has a specific responsibility.

| Layer      | Responsibility        |
| ---------- | --------------------- |
| Controller | Handles HTTP requests |
| Service    | Business logic        |
| Repository | Data access           |
| Model      | Data structure        |

---

# 1. Create the Model

Create a new package:

```
model
```

Create the file:

```
User.java
```

Add the following code:

```java
package com.example.helloservice.model;

public class User {

    private Long id;
    private String name;
    private String email;

    public User() {}

    public User(Long id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

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

This class represents the data structure of a user.

---

# 2. Create the Repository Layer

Create a package:

```
repository
```

Create the file:

```
UserRepository.java
```

Add the code:

```java
package com.example.helloservice.repository;

import com.example.helloservice.model.User;
import org.springframework.stereotype.Repository;

import java.util.ArrayList;
import java.util.List;

@Repository
public class UserRepository {

    private final List<User> users = new ArrayList<>();

    public List<User> findAll() {
        return users;
    }

    public void save(User user) {
        users.add(user);
    }
}
```

For now, we are using in-memory storage instead of a real database.

Later this can be replaced with Spring Data JPA.

---

# 3. Create the Service Layer

Create a package:

```
service
```

Create the file:

```
UserService.java
```

Add the following code:

```java
package com.example.helloservice.service;

import com.example.helloservice.model.User;
import com.example.helloservice.repository.UserRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    public void createUser(User user) {
        userRepository.save(user);
    }
}
```

The service layer contains business logic.

It acts as a bridge between the controller and the repository.

---

# 4. Create the Controller Layer

Create a package:

```
controller
```

Create the file:

```
UserController.java
```

Add the code:

```java
package com.example.helloservice.controller;

import com.example.helloservice.model.User;
import com.example.helloservice.service.UserService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public List<User> getUsers() {
        return userService.getAllUsers();
    }

    @PostMapping
    public String createUser(@RequestBody User user) {
        userService.createUser(user);
        return "User created successfully";
    }
}
```

This controller exposes REST APIs.

Endpoints:

| Method | Endpoint | Description   |
| ------ | -------- | ------------- |
| GET    | /users   | Get all users |
| POST   | /users   | Create a user |

---

# Run the Application

Start the application as before.

Run the main class:

```
HelloServiceApplication.java
```

Or use the terminal:

```
./mvnw spring-boot:run
```

---

# Test the API

## Get Users

Open a browser or Postman:

```
http://localhost:8080/users
```

Response:

```
[]
```

---

## Create User

POST request:

```
http://localhost:8080/users
```

Body:

```json
{
  "id": 1,
  "name": "Sahil",
  "email": "sahil@example.com"
}
```

Response:

```
User created successfully
```

Now call the endpoint again:

```
GET /users
```

Response:

```json
[
  {
    "id": 1,
    "name": "Sahil",
    "email": "sahil@example.com"
  }
]
```

---

# Why This Architecture Matters

Separating layers provides several benefits.

Clean Code
Controllers remain small and focused.

Reusable Logic
Business logic is centralized in the service layer.

Testability
Each layer can be tested independently.

Scalability
Large systems require a structured architecture.

---
