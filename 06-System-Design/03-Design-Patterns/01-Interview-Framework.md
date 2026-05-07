# System Design Interview Framework

## Table of Contents
1. [Approach](#approach)
2. [Requirements Analysis](#requirements-analysis)
3. [Architecture](#architecture)
4. [Deep Dive](#deep-dive)
5. [Bottlenecks](#bottlenecks)
6. [Scaling](#scaling)

---

## Approach

### Timeline: 45 minutes interview

```
5 mins  - Clarification
5 mins  - Capacity Estimation  
10 mins - High-level Design
15 mins - Deep Dive
5 mins  - Bottlenecks & Scaling
5 mins  - Final Q&A
```

---

## Requirements Analysis

### Functional Requirements
**What the system should do**

```
Example: Design Twitter
- Users can post tweets (140-280 chars)
- Users can follow/unfollow other users
- Users can see feed of followed users
- Users can search tweets
- Users can like/retweet
```

### Non-Functional Requirements
**How the system should behave**

```
- Scalability: Handle millions of users
- Availability: 99.9% uptime (3 nines)
- Latency: Feed loads in < 200ms
- Consistency: Eventually consistent is OK
- Durability: Data persists
```

### Capacity Estimation

```
Example: Twitter-like system

Users: 300 million
Daily Active Users: 100 million
Tweets per user per day: 2
Total tweets per day: 200 million
Tweets per second: 200M / 86400 = ~2,300 QPS

Peak QPS: 2,300 * 3 = 6,900 QPS

Read:Write ratio = 100:1 (mostly reading feeds)
Read QPS: ~690,000
Write QPS: ~6,900

Storage per tweet: 300 bytes
Daily storage: 200M * 300 = 60 GB
Yearly storage: 60GB * 365 = 21.9 TB

Bandwidth:
Write: 6,900 * 300 = 2 MB/s
Read: 690,000 * 300 = 207 MB/s (peak)
```

---

## Architecture

### High-Level Design

```
┌─────────────┐
│   Clients   │ (Web, Mobile, API)
└──────┬──────┘
       │
       ▼
┌─────────────────┐
│  Load Balancer  │ (nginx, AWS ELB)
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌──────┐   ┌──────┐
│API-1 │   │API-2 │  (Web Servers)
└──┬───┘   └──┬───┘
   │          │
   └────┬─────┘
        ▼
┌──────────────┐
│  Cache      │ (Redis, Memcached)
└──────┬───────┘
       │
       ▼
┌──────────────────┐
│  Database        │ (MySQL, PostgreSQL)
│  - Primary       │
│  - Replicas      │
└──────────────────┘

┌──────────────┐
│ Message Queue│ (Kafka, RabbitMQ)
└──────────────┘

┌──────────────┐
│ Search       │ (Elasticsearch)
│ Service      │
└──────────────┘
```

### Components

#### 1. API Servers
- Stateless (can scale horizontally)
- Handle request routing
- Authentication/Authorization

#### 2. Cache Layer
- Reduce database load
- Improve response time
- Popular data: user profiles, timelines

#### 3. Database
- Primary (writes)
- Replicas (reads)
- Sharding for scalability

#### 4. Message Queue
- Asynchronous processing
- Decoupling services
- Example: Tweet notifications

#### 5. Search Service
- Full-text search
- Elasticsearch for tweets
- Fast querying

---

## Deep Dive

### Example: Design Twitter Feed

#### Approach 1: Pull Model
```
User requests feed
    ↓
Fetch all followed users' tweets
    ↓
Sort by timestamp (DESC)
    ↓
Return top 100 tweets

Pros: Simple, fresh data
Cons: Slow (N queries), high latency
```

#### Approach 2: Push Model (Fan-out)
```
When user tweets:
    ↓
Find all followers
    ↓
Add tweet to each follower's timeline cache
    ↓
User sees pre-computed timeline

Pros: Fast reads, cached
Cons: Write heavy, storage for inactive users
```

#### Approach 3: Hybrid (Recommended)
```
Push for active users (<10K followers)
Pull for celebrities (>10K followers)

Combines benefits of both
```

---

## Bottlenecks

### Database Bottleneck
```
Problem: Single database gets overloaded

Solutions:
1. Read replicas
2. Sharding (by user_id, region, etc.)
3. Caching layer
```

### Cache Invalidation
```
Problem: Stale cache data

Strategies:
1. TTL (Time To Live)
2. Active invalidation (delete on update)
3. Event-based invalidation
```

### Single Point of Failure
```
Problem: Load balancer fails

Solutions:
1. Multiple load balancers
2. DNS failover
3. Health checks
```

---

## Scaling

### Horizontal Scaling
```
Add more API servers
    ↓
Load balancer distributes
    ↓
Stateless makes this easy
```

### Database Scaling
```
Read replicas:
  Primary → Replica 1
       → Replica 2
       → Replica 3

Sharding:
  User 1-100K → Shard 1
  User 100K-200K → Shard 2
  User 200K-300K → Shard 3
```

### Caching Strategy
```
1. Cache popular content
2. Cache user profiles
3. Cache timeline for top 10% users
```

---

## Common Metrics

### Availability
```
99% = 3.65 days downtime/year
99.9% = 8.76 hours downtime/year (3 nines)
99.99% = 52.6 minutes downtime/year (4 nines)
```

### Latency
```
< 100ms   = Excellent
100-500ms = Good
> 500ms   = Poor
```

### Throughput
```
QPS = Queries Per Second
TPS = Transactions Per Second
```

---

## Interview Tips

### Do's
✅ Ask clarification questions  
✅ Start high-level, drill down  
✅ Discuss trade-offs  
✅ Mention monitoring/logging  
✅ Consider failure scenarios  
✅ Talk about cost  

### Don'ts
❌ Jump to implementation  
❌ Over-engineer  
❌ Ignore scalability  
❌ Assume perfect conditions  
❌ Forget about data consistency  
❌ Miss edge cases  

---

## Interview Questions

### Q1: How do you handle cache invalidation?
**Answer:** Use TTL, active invalidation, or event-based strategies. For consistency-critical data, use shorter TTLs.

### Q2: How do you ensure high availability?
**Answer:** Multiple replicas, load balancing, database replication, and failover mechanisms.

### Q3: What's your sharding strategy?
**Answer:** Depends on access patterns. Common: user_id based for user-centric systems.

### Q4: How do you handle rate limiting?
**Answer:** Token bucket, sliding window, or leaky bucket algorithms. Store in cache layer for fast lookup.

### Q5: How do you monitor system health?
**Answer:** Logging, metrics (Prometheus), tracing (Jaeger), alerting systems.
