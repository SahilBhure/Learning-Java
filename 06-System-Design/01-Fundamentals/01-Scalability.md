# Scalability in System Design

## Table of Contents
1. [What is Scalability?](#what-is-scalability)
2. [Types of Scalability](#types-of-scalability)
3. [Scaling Strategies](#scaling-strategies)
4. [Load Balancing](#load-balancing)
5. [Best Practices](#best-practices)

---

## What is Scalability?

Scalability is the ability of a system to handle increased load without significant performance degradation.

### Three Dimensions

```
┌──────────────────────────────────────────┐
│          System Scalability              │
├──────────────────────────────────────────┤
│  1. Vertical Scaling (Scale Up)          │
│  2. Horizontal Scaling (Scale Out)       │
│  3. Diagonal Scaling (Both)              │
└──────────────────────────────────────────┘
```

---

## Types of Scalability

### 1. Vertical Scaling (Scale Up)
Adding more resources to a single server.

```
Before:              After:
Server               Server
4GB RAM              16GB RAM
2 CPU               8 CPU
1TB Disk            4TB Disk
```

#### Advantages
- Simple to implement
- No code changes needed
- Still uses single database

#### Disadvantages
- Hardware limits
- Single point of failure
- High cost per resource
- Downtime required for upgrade

#### When to Use
- Early stage startups
- Simple applications
- Short-term growth

### 2. Horizontal Scaling (Scale Out)
Adding more servers to handle load.

```
Before:              After:
Server1              Server1
                     Server2
                     Server3
                     Load Balancer
```

#### Advantages
- No hardware limits
- Fault tolerance
- Can grow indefinitely
- Distributed

#### Disadvantages
- Complex implementation
- Network communication overhead
- Database becomes bottleneck
- Requires careful design

#### When to Use
- High traffic applications
- Large-scale systems
- Long-term growth
- FAANG companies

### 3. Diagonal Scaling (Combined)
Combination of vertical and horizontal scaling.

```
Phase 1: Vertical Scaling
Server 8GB RAM 2CPU
        ↓ (Growth)
        
Phase 2: Horizontal Scaling
Server1 (8GB, 2CPU) → Load Balancer ← Server2 (8GB, 2CPU)
        ↓                              ↓
     Database                      Database Replication
```

---

## Scaling Strategies

### 1. Database Scaling

#### Read Replicas
```
Primary DB (Write)
    ↓
Replica 1 (Read)
Replica 2 (Read)
Replica 3 (Read)
```

```java
// Write to primary
Database.write(data);  // Primary DB

// Read from replicas
Database.read();       // Replica 1
Database.read();       // Replica 2
```

#### Sharding
Partition data across multiple databases.

```
Shard Key: user_id % 3

User 1,4,7 → Shard 1
User 2,5,8 → Shard 2
User 3,6,9 → Shard 3
```

### 2. Caching Layer

```
Client Request
    ↓
Cache (Redis/Memcached) ← Check first
    ↓ (if miss)
Database
```

```java
// Pseudo-code
public User getUser(Long id) {
    // Check cache first
    User user = cache.get("user:" + id);
    
    if (user == null) {
        // Not in cache, fetch from DB
        user = database.findById(id);
        // Store in cache
        cache.put("user:" + id, user);
    }
    
    return user;
}
```

### 3. Message Queue

```
Client Request
    ↓
Producer → Queue (Kafka/RabbitMQ)
              ↓
           Consumer 1
           Consumer 2
           Consumer 3
```

---

## Load Balancing

Distributes traffic across multiple servers.

### Algorithms

#### 1. Round Robin
Distribute requests equally.

```
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 3
Request 4 → Server 1
```

#### 2. Least Connection
Route to server with fewest connections.

```
Server 1: 10 connections
Server 2: 5 connections  ← Route here
Server 3: 8 connections
```

#### 3. IP Hash
Route based on client IP.

```
Hash(Client IP) % num_servers = server_id
// Same client always goes to same server
```

#### 4. Weighted Round Robin
Distribute based on server capacity.

```
Server 1 (weight: 3) → 3 requests
Server 2 (weight: 2) → 2 requests
Server 3 (weight: 1) → 1 request
```

### Load Balancer Examples
- AWS Elastic Load Balancer
- Nginx
- HAProxy
- F5 BIG-IP

---

## Best Practices

### 1. Design for Scalability from Start
```java
// Good: Stateless service
@RestController
public class UserController {
    @Autowired
    private UserService service;
    
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) {
        return service.getUser(id);
    }
    // No session data stored in service
}

// Bad: Stateful service
public class UserSession {
    private User currentUser;  // Ties to specific server
    
    public void setUser(User user) {
        this.currentUser = user;  // Hard to scale
    }
}
```

### 2. Use Caching Strategically
```java
@Service
public class ProductService {
    @Cacheable("products")
    public Product getProduct(Long id) {
        return productRepository.findById(id).orElse(null);
    }
    
    @CacheEvict("products", allEntries = true)
    public void updateProduct(Product product) {
        productRepository.save(product);
    }
}
```

### 3. Database Indexing
```sql
-- Index frequently queried columns
CREATE INDEX idx_email ON users(email);
CREATE INDEX idx_user_id_created ON orders(user_id, created_at);
```

### 4. Asynchronous Processing
```java
@Service
public class OrderService {
    @Async
    public void processOrder(Order order) {
        // Long operation on separate thread
        // Doesn't block main request
    }
}
```

---

## Interview Questions

### Q1: Explain horizontal vs vertical scaling?
**Answer:** Vertical = adding resources to one server, Horizontal = adding more servers. Horizontal is preferred for large systems.

### Q2: What are database replicas used for?
**Answer:** Read replicas handle read queries, reducing load on primary which handles writes. Improves performance.

### Q3: What's the purpose of a load balancer?
**Answer:** Distributes incoming traffic across multiple servers, preventing any single server from being overloaded.

### Q4: When should you use caching?
**Answer:** Cache frequently accessed, rarely changing data. Use for expensive queries or computations.

### Q5: What's sharding?
**Answer:** Partitioning data across multiple databases based on a key. Allows infinite horizontal scaling of data.
