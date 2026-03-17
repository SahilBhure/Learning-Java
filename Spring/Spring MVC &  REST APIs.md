
## Spring MVC & REST APIs (Web Layer)

---

## 1. What is Spring MVC?

Spring MVC is a **web framework** based on:

> **Model-View-Controller (MVC) design pattern**

---

## 2. MVC Architecture

```text
Client → Controller → Service → Repository → Database
             ↓
           Response
```

---

### Components:

| Component  | Role             |
| ---------- | ---------------- |
| Model      | Data             |
| View       | UI (HTML/JSON)   |
| Controller | Handles requests |

---

## 3. REST APIs in Spring

REST = Representational State Transfer

Used for:

* Frontend ↔ Backend communication
* Microservices

---

## 4. @RestController (Most Important)

```java id="1a9c8x"
@RestController
@RequestMapping("/users")
public class UserController {
}
```

Combines:

* `@Controller`
* `@ResponseBody`

---

## 5. Handling HTTP Methods

### GET

```java id="2b8d7y"
@GetMapping
public List<User> getUsers() {
    return userService.getAllUsers();
}
```

---

### POST

```java id="3c7e6z"
@PostMapping
public User createUser(@RequestBody User user) {
    return userService.save(user);
}
```

---

### PUT

```java id="4d6f5a"
@PutMapping("/{id}")
public User update(@PathVariable Long id, @RequestBody User user) {
    return userService.update(id, user);
}
```

---

### DELETE

```java id="5e5g4b"
@DeleteMapping("/{id}")
public void delete(@PathVariable Long id) {
    userService.delete(id);
}
```

---

## 6. Request Handling Annotations

### @RequestBody

* Converts JSON → Java Object

### @PathVariable

```java id="6f4h3c"
@GetMapping("/{id}")
public User getUser(@PathVariable Long id) {
}
```

---

### @RequestParam

```java id="7g3i2d"
@GetMapping("/search")
public List<User> search(@RequestParam String name) {
}
```

---

## 7. Response Handling

### Returning JSON

Spring automatically converts:

> Java Object → JSON

---

### ResponseEntity (Best Practice)

```java id="8h2j1e"
return ResponseEntity.ok(user);
```

Custom response:

```java id="9i1k0f"
return ResponseEntity.status(HttpStatus.CREATED).body(user);
```

---

## 8. Exception Handling

### @ExceptionHandler

```java id="0j9l8g"
@ExceptionHandler(Exception.class)
public ResponseEntity<String> handleError(Exception ex) {
    return ResponseEntity.badRequest().body(ex.getMessage());
}
```

---

### Global Exception Handler

```java id="1k8m7h"
@ControllerAdvice
public class GlobalExceptionHandler {
}
```

---

## 9. Validation

### @Valid

```java id="2l7n6i"
@PostMapping
public User create(@Valid @RequestBody User user) {
}
```

---

### Example

```java id="3m6o5j"
@NotNull
private String name;
```

---

## 10. DTO Pattern (Important)

Instead of exposing entities:

```java id="4n5p4k"
public class UserDTO {
    private String name;
}
```

Why:

* Security
* Flexibility
* Clean API

---

## 11. Layered Architecture (Real-World)

```text
Controller → Service → Repository
```

Example:

```java id="5o4q3l"
@RestController
public class UserController {

    private final UserService service;

    public UserController(UserService service) {
        this.service = service;
    }
}
```

---

## 12. REST API Best Practices

* Use proper HTTP methods
* Use status codes correctly
* Use DTOs
* Keep controllers thin
* Handle exceptions globally

---

## 13. Common Mistakes

* Putting business logic in controller
* Returning entities directly
* Not validating input
* Poor API design

---

## 14. Example API Endpoints

```text
GET     /users
GET     /users/{id}
POST    /users
PUT     /users/{id}
DELETE  /users/{id}
```

---

## 15. Testing APIs

Use tools:

* Postman
* Curl

Example:

```bash id="6p3r2m"
curl -X GET http://localhost:8080/users
```

