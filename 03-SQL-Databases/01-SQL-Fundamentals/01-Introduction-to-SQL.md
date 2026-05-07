# Introduction to SQL

## Table of Contents
1. [What is SQL?](#what-is-sql)
2. [Database Types](#database-types)
3. [SQL Basics](#sql-basics)
4. [Common SQL Commands](#common-sql-commands)
5. [Best Practices](#best-practices)

---

## What is SQL?

SQL (Structured Query Language) is a standard language for managing relational databases. It allows you to:
- Create and modify database structures
- Insert, update, and delete data
- Query and retrieve data
- Control access to database
- Perform complex data analysis

### Why Learn SQL?
- Universal skill - works across all relational databases
- Essential for data analysis and reporting
- Foundation for backend development
- Interview requirement for most tech companies

---

## Database Types

### Relational Databases (SQL)
- MySQL
- PostgreSQL
- Oracle
- SQL Server
- MariaDB

### NoSQL Databases
- MongoDB
- Cassandra
- Redis
- DynamoDB

---

## SQL Basics

### Database Structure
```
Database
├── Table 1 (users)
│   ├── Column 1 (id)
│   ├── Column 2 (name)
│   └── Column 3 (email)
├── Table 2 (orders)
│   ├── Column 1 (order_id)
│   ├── Column 2 (user_id)
│   └── Column 3 (amount)
```

### Key Concepts

#### Table
A collection of rows and columns.

#### Row/Record
A single entry in a table.

#### Column/Field
A characteristic of the data.

#### Primary Key
Unique identifier for each row.

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,        -- Primary key
    name VARCHAR(100),
    email VARCHAR(100),
    age INT
);
```

#### Foreign Key
Link to another table's primary key.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    amount DECIMAL(10, 2),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

---

## Common SQL Commands

### DDL (Data Definition Language)
Define database structure.

```sql
-- CREATE: Create table
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- ALTER: Modify table
ALTER TABLE users ADD COLUMN phone VARCHAR(15);
ALTER TABLE users DROP COLUMN phone;
ALTER TABLE users MODIFY COLUMN name VARCHAR(150);

-- DROP: Delete table
DROP TABLE users;

-- TRUNCATE: Delete all rows but keep structure
TRUNCATE TABLE users;
```

### DML (Data Manipulation Language)
Manipulate data in tables.

```sql
-- INSERT: Add new rows
INSERT INTO users (name, email, age) 
VALUES ('John', 'john@example.com', 25);

INSERT INTO users (name, email, age) 
VALUES 
    ('Jane', 'jane@example.com', 30),
    ('Bob', 'bob@example.com', 28);

-- UPDATE: Modify existing rows
UPDATE users SET age = 26 WHERE name = 'John';
UPDATE users SET age = age + 1;  -- All rows

-- DELETE: Remove rows
DELETE FROM users WHERE id = 1;
DELETE FROM users;  -- All rows
```

### DQL (Data Query Language)
Retrieve data.

```sql
-- SELECT: Retrieve data
SELECT * FROM users;  -- All columns
SELECT name, email FROM users;  -- Specific columns
SELECT DISTINCT age FROM users;  -- Unique values
```

### DCL (Data Control Language)
Control access permissions.

```sql
-- GRANT: Give permissions
GRANT SELECT, INSERT ON users TO user1;

-- REVOKE: Remove permissions
REVOKE DELETE ON users FROM user1;
```

---

## SQL Clauses

### WHERE
Filter rows based on conditions.

```sql
SELECT * FROM users WHERE age > 25;
SELECT * FROM users WHERE name = 'John';
SELECT * FROM users WHERE age > 25 AND city = 'NYC';
```

### ORDER BY
Sort results.

```sql
SELECT * FROM users ORDER BY age;        -- Ascending
SELECT * FROM users ORDER BY age DESC;   -- Descending
SELECT * FROM users ORDER BY age, name;  -- Multiple columns
```

### LIMIT
Restrict number of rows returned.

```sql
SELECT * FROM users LIMIT 10;      -- First 10 rows
SELECT * FROM users LIMIT 10 OFFSET 5;  -- Skip 5, take 10
```

---

## Data Types

### Numeric
```sql
INT              -- Integer
DECIMAL(10, 2)  -- Decimal with 10 digits, 2 after decimal
FLOAT            -- Floating point
BOOLEAN          -- True/False
```

### String
```sql
VARCHAR(100)    -- Variable length (0-100 characters)
CHAR(10)        -- Fixed length (always 10 characters)
TEXT            -- Large text
```

### Date/Time
```sql
DATE             -- 'YYYY-MM-DD'
TIME             -- 'HH:MM:SS'
TIMESTAMP        -- 'YYYY-MM-DD HH:MM:SS'
DATETIME        -- Date and time
```

---

## Constraints

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,           -- Cannot be null
    email VARCHAR(100) UNIQUE,            -- Must be unique
    age INT CHECK (age >= 18),            -- Must satisfy condition
    city VARCHAR(50) DEFAULT 'NYC',       -- Default value
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Best Practices

### 1. Use Meaningful Names
```sql
-- Good
SELECT customer_name, customer_email FROM customers;

-- Bad
SELECT c_n, c_e FROM cust;
```

### 2. Use Prepared Statements (Prevent SQL Injection)
```sql
-- Vulnerable to SQL injection
SELECT * FROM users WHERE id = " + id;

-- Safe with prepared statements
PreparedStatement ps = connection.prepareStatement(
    "SELECT * FROM users WHERE id = ?");
ps.setInt(1, id);
```

### 3. Use Appropriate Data Types
```sql
-- Good
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10, 2),
    quantity INT,
    is_active BOOLEAN
);
```

### 4. Index Frequently Queried Columns
```sql
CREATE INDEX idx_email ON users(email);
CREATE INDEX idx_name ON users(name);
```

### 5. Comment Your Queries
```sql
-- Get all active users with orders in last month
SELECT u.id, u.name, COUNT(o.id) as order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE u.is_active = 1
AND o.created_at >= DATE_SUB(NOW(), INTERVAL 1 MONTH);
```

---

## Interview Questions

### Q1: What's the difference between SQL and NoSQL?
**Answer:** SQL is relational (structured tables), NoSQL is non-relational (flexible documents). Use SQL for structured data, NoSQL for flexible/unstructured data.

### Q2: What's a primary key?
**Answer:** A unique identifier for each row in a table. Cannot be NULL and must be unique.

### Q3: What's a foreign key?
**Answer:** A column that references another table's primary key. Maintains referential integrity.

### Q4: What are constraints?
**Answer:** Rules applied to columns: PRIMARY KEY, FOREIGN KEY, NOT NULL, UNIQUE, CHECK, DEFAULT.
