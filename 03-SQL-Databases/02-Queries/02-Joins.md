# Joins in SQL

## Table of Contents
1. [INNER JOIN](#inner-join)
2. [LEFT JOIN](#left-join)
3. [RIGHT JOIN](#right-join)
4. [FULL OUTER JOIN](#full-outer-join)
5. [CROSS JOIN](#cross-join)
6. [Self Join](#self-join)
7. [Complex Joins](#complex-joins)

---

## Visual Representation

```
Table A       Table B
ID Name       ID Score
1  John       1  90
2  Jane       2  85
3  Bob        4  95

Inner Join (Common): 1,2
Left Join (All A): 1,2,3
Right Join (All B): 1,2,4
Full Outer (All): 1,2,3,4
```

---

## INNER JOIN

Returns rows that have matches in both tables.

### Syntax
```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

### Example
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    amount DECIMAL(10, 2)
);

INSERT INTO users VALUES (1, 'John'), (2, 'Jane'), (3, 'Bob');
INSERT INTO orders VALUES (101, 1, 100), (102, 2, 200), (103, 1, 150);

-- INNER JOIN
SELECT users.id, users.name, orders.amount
FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- Result:
-- id | name | amount
-- 1  | John | 100
-- 1  | John | 150
-- 2  | Jane | 200
```

### Using Aliases
```sql
SELECT u.id, u.name, o.amount
FROM users u
INNER JOIN orders o ON u.id = o.user_id;
```

---

## LEFT JOIN

Returns all rows from left table, matched rows from right table.

### Syntax
```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

### Example
```sql
SELECT u.id, u.name, COUNT(o.order_id) as order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name;

-- Result (includes Bob with 0 orders):
-- id | name | order_count
-- 1  | John | 2
-- 2  | Jane | 1
-- 3  | Bob  | 0
```

### Finding Records Without Match
```sql
-- Users with no orders
SELECT u.id, u.name
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE o.order_id IS NULL;

-- Result:
-- id | name
-- 3  | Bob
```

---

## RIGHT JOIN

Returns all rows from right table, matched rows from left table.

### Example
```sql
SELECT u.id, u.name, o.amount
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;

-- Includes all orders, some users might be NULL
```

### Note
Most databases support LEFT JOIN. RIGHT JOIN can be rewritten as LEFT JOIN:

```sql
-- These are equivalent:
SELECT *
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;

-- Same as:
SELECT *
FROM orders o
LEFT JOIN users u ON u.id = o.user_id;
```

---

## FULL OUTER JOIN

Returns all rows from both tables.

### Syntax
```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

### Example
```sql
SELECT u.id, u.name, o.amount
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;

-- Result (some users or orders might have NULL):
-- id   | name | amount
-- 1    | John | 100
-- 1    | John | 150
-- 2    | Jane | 200
-- 3    | Bob  | NULL
-- NULL | NULL | (if there are unmatched orders)
```

### Note
MySQL doesn't support FULL OUTER JOIN directly. Use UNION:

```sql
-- FULL OUTER JOIN using UNION
SELECT u.id, u.name, o.amount
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
UNION
SELECT u.id, u.name, o.amount
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```

---

## CROSS JOIN

Returns Cartesian product (all combinations).

### Syntax
```sql
SELECT column_name(s)
FROM table1
CROSS JOIN table2;
```

### Example
```sql
CREATE TABLE colors (id INT, color VARCHAR(50));
CREATE TABLE sizes (id INT, size VARCHAR(10));

INSERT INTO colors VALUES (1, 'Red'), (2, 'Blue');
INSERT INTO sizes VALUES (1, 'S'), (2, 'M'), (3, 'L');

SELECT c.color, s.size
FROM colors c
CROSS JOIN sizes s;

-- Result (2 * 3 = 6 rows):
-- color | size
-- Red   | S
-- Red   | M
-- Red   | L
-- Blue  | S
-- Blue  | M
-- Blue  | L
```

---

## Self Join

Joining a table with itself.

### Example: Employee-Manager Relationship
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    manager_id INT
);

INSERT INTO employees VALUES
(1, 'John', NULL),
(2, 'Jane', 1),
(3, 'Bob', 1),
(4, 'Alice', 2);

-- Find employees and their managers
SELECT e.name as employee, m.name as manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.employee_id;

-- Result:
-- employee | manager
-- John     | NULL
-- Jane     | John
-- Bob      | John
-- Alice    | Jane
```

---

## Complex Joins

### Multiple Joins
```sql
SELECT u.name, o.order_id, p.product_name, od.quantity
FROM users u
INNER JOIN orders o ON u.id = o.user_id
INNER JOIN order_items od ON o.order_id = od.order_id
INNER JOIN products p ON od.product_id = p.product_id;
```

### Join with WHERE Clause
```sql
SELECT u.name, COUNT(o.order_id) as order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE u.created_at > '2024-01-01'
GROUP BY u.id, u.name
HAVING COUNT(o.order_id) > 0;
```

### Join with Subquery
```sql
SELECT u.name, sub.total_amount
FROM users u
INNER JOIN (
    SELECT user_id, SUM(amount) as total_amount
    FROM orders
    GROUP BY user_id
) sub ON u.id = sub.user_id;
```

---

## Join Comparison

| Join Type | Left Table | Right Table | Result |
|-----------|-----------|-------------|--------|
| INNER | Matched | Matched | Only matches |
| LEFT | All | Matched | All left + matches |
| RIGHT | Matched | All | Matches + all right |
| FULL | All | All | All from both |
| CROSS | All | All | All combinations |

---

## Interview Questions

### Q1: What's the difference between INNER JOIN and LEFT JOIN?
**Answer:** INNER JOIN returns only matching rows. LEFT JOIN returns all rows from left table plus matching rows from right table.

### Q2: How to find unmatched records?
**Answer:** Use LEFT JOIN with WHERE IS NULL on right table columns.

### Q3: Can you join more than 2 tables?
**Answer:** Yes, you can chain multiple JOINs.

### Q4: What's the performance impact of different joins?
**Answer:** INNER JOIN is usually fastest. Complex joins can be slow. Always index join columns.

### Q5: When would you use CROSS JOIN?
**Answer:** For generating all combinations (e.g., product sizes with colors).
