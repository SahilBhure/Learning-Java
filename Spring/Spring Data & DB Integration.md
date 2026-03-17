
## Spring Data & Database Integration (JDBC, JPA, Transactions)

---


## 2. Challenges Without Spring

Using plain JDBC:

```java id="1a2b3c"
Connection conn = DriverManager.getConnection(...);
PreparedStatement ps = conn.prepareStatement(...);
ResultSet rs = ps.executeQuery();
```

Problems:

* Boilerplate code
* Manual resource handling
* Error-prone
* Hard to maintain

---

## 3. Spring JDBC (Simplified JDBC)

Spring provides:

> **JdbcTemplate**

---

### Example:

```java id="4d5e6f"
@Autowired
private JdbcTemplate jdbcTemplate;

public List<String> getUsers() {
    return jdbcTemplate.query(
        "SELECT name FROM users",
        (rs, rowNum) -> rs.getString("name")
    );
}
```

Benefits:

* No manual connection handling
* Cleaner code
* Exception handling simplified

---

## 4. ORM (Object Relational Mapping)

ORM maps:

> Java Objects ↔ Database Tables

Popular ORM:

* Hibernate

---

## 5. JPA (Java Persistence API)

JPA is:

> A specification (not implementation)

Hibernate is:

> Implementation of JPA

---

## 6. Spring Data JPA (Most Important)

Spring Data JPA:

> Reduces database code drastically

---

### Example Entity

```java id="7g8h9i"
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;
}
```

---

### Repository Interface

```java id="0j1k2l"
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

That’s it. Spring provides:

* CRUD operations
* Pagination
* Sorting

---

## 7. Custom Queries

### Method Naming

```java id="3m4n5o"
List<User> findByName(String name);
```

Spring automatically generates query.

---

### @Query Annotation

```java id="6p7q8r"
@Query("SELECT u FROM User u WHERE u.name = :name")
List<User> findUsers(@Param("name") String name);
```

---

## 8. Transaction Management (VERY IMPORTANT)

### What is a Transaction?

A transaction ensures:

> **All operations succeed OR none do**

---

### Example Problem

```java id="9s0t1u"
withdrawMoney();
depositMoney();
```

If deposit fails → inconsistent data

---

## 9. @Transactional Annotation

```java id="2v3w4x"
@Transactional
public void transferMoney() {
    withdraw();
    deposit();
}
```

Spring ensures:

* Atomicity
* Consistency
* Rollback on failure

---

## 10. How Transactions Work Internally

Spring uses:

* AOP (proxies)
* PlatformTransactionManager

Flow:

1. Method called
2. Proxy intercepts
3. Transaction starts
4. Method executes
5. Commit or rollback

---

## 11. Transaction Propagation

Defines how transactions behave when nested:

| Type         | Description            |
| ------------ | ---------------------- |
| REQUIRED     | Default, join existing |
| REQUIRES_NEW | Create new             |
| SUPPORTS     | Use if exists          |

Example:

```java id="5y6z7a"
@Transactional(propagation = Propagation.REQUIRES_NEW)
```

---

## 12. Isolation Levels

Control data consistency:

| Level            | Description         |
| ---------------- | ------------------- |
| READ_UNCOMMITTED | Dirty reads allowed |
| READ_COMMITTED   | Default             |
| REPEATABLE_READ  | Prevent updates     |
| SERIALIZABLE     | Highest safety      |

---

## 13. Rollback Rules

By default:

* Rolls back on RuntimeException

Custom:

```java id="8b9c0d"
@Transactional(rollbackFor = Exception.class)
```

---

## 14. Spring Boot Database Config (Quick View)

```properties id="1e2f3g"
spring.datasource.url=jdbc:mysql://localhost:3306/db
spring.datasource.username=root
spring.datasource.password=pass

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

## 15. Real-World Architecture

```id="4h5i6j"
Controller → Service → Repository → Database
```

* Controller → API layer
* Service → Business logic + transactions
* Repository → DB access

---

## 16. Common Mistakes

* Using @Transactional on private methods
* Not understanding propagation
* Mixing JDBC and JPA incorrectly
* Ignoring lazy loading issues

---

## 17. Best Practices

* Use Spring Data JPA
* Keep transactions in service layer
* Use DTOs for data transfer
* Avoid business logic in repositories

---
