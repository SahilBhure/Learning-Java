# 1. What is SQL?

SQL (Structured Query Language) is used to **communicate with relational databases**.

You use SQL to:

* Store data
* Retrieve data
* Update data
* Delete data
* Manage database structure

---

# 2. What is a Database?

A database is a structured collection of data.

Example:

| id | name  | role      |
| -- | ----- | --------- |
| 1  | Sahil | Developer |
| 2  | John  | Tester    |

This data is stored in **tables**.

---

# 3. What is a Table?

A table consists of:

* Rows → records
* Columns → attributes

Example:

Table: `users`

| id | name | email |
| -- | ---- | ----- |

---

# 4. SQL Categories

SQL commands are grouped into:

---

## DDL (Data Definition Language)

Used to define structure

* CREATE
* ALTER
* DROP
* TRUNCATE

---

## DML (Data Manipulation Language)

Used to modify data

* INSERT
* UPDATE
* DELETE

---

## DQL (Data Query Language)

Used to retrieve data

* SELECT

---

## DCL (Data Control Language)

* GRANT
* REVOKE

---

## TCL (Transaction Control Language)

* COMMIT
* ROLLBACK
* SAVEPOINT

---

# 5. First SQL Query

```sql
SELECT * FROM users;
```

Meaning:

* SELECT → choose columns
* * → all columns
* FROM → table name

---

# 6. Selecting Specific Columns

```sql
SELECT id, name FROM users;
```

---

# 7. SQL is Case Insensitive

These are same:

```sql
select * from users;
SELECT * FROM users;
Select * From users;
```

---

# 8. SQL Execution Order (Important)

Logical execution order:

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY
7. LIMIT

This is crucial for advanced queries.

---

# 9. Example Table We'll Use

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(50),
    salary INT,
    department VARCHAR(50)
);
```

---

# 10. Insert Data

```sql
INSERT INTO employees VALUES (1, 'Sahil', 50000, 'IT');
INSERT INTO employees VALUES (2, 'Rahul', 60000, 'HR');
INSERT INTO employees VALUES (3, 'Amit', 70000, 'IT');
```

---

# 11. View Data

```sql
SELECT * FROM employees;
```

---

# 12. Filter Data

```sql
SELECT * FROM employees
WHERE department = 'IT';
```

---

# 13. Why SQL is Important for Interviews

Backend interviews often test:

* Joins
* Aggregations
* Group By
* Subqueries
* Window functions
* Indexing
* Query optimization

---

# 14. SQL Mastery Path

We will cover:

1. SELECT Deep Dive
2. WHERE Conditions
3. Sorting & Limiting
4. Aggregations
5. GROUP BY & HAVING
6. JOINS (Very Important)
7. Subqueries
8. Window Functions (Advanced)
9. Indexing
10. Query Optimization
11. Transactions
12. Interview Problems
