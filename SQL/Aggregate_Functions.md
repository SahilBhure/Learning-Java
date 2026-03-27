# Aggregate Functions

Aggregate functions operate on **multiple rows** and return **single value**.

---

# Most Important Aggregate Functions

| Function | Description |
| -------- | ----------- |
| COUNT()  | Count rows  |
| SUM()    | Total sum   |
| AVG()    | Average     |
| MIN()    | Minimum     |
| MAX()    | Maximum     |

---

# COUNT()

Counts number of rows.

```sql
SELECT COUNT(*)
FROM employees;
```

Counts all rows including NULL.

---

# COUNT Column

```sql
SELECT COUNT(salary)
FROM employees;
```

Counts only **non-null salary values**.

---

# COUNT DISTINCT

```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```

Counts unique departments.

---

# SUM()

```sql
SELECT SUM(salary)
FROM employees;
```

Total salary.

---

# AVG()

```sql
SELECT AVG(salary)
FROM employees;
```

Average salary.

---

# MIN()

```sql
SELECT MIN(salary)
FROM employees;
```

Lowest salary.

---

# MAX()

```sql
SELECT MAX(salary)
FROM employees;
```

Highest salary.

---

# Multiple Aggregates Together

```sql
SELECT 
    COUNT(*),
    SUM(salary),
    AVG(salary),
    MIN(salary),
    MAX(salary)
FROM employees;
```

---

# Aggregate with WHERE

```sql
SELECT COUNT(*)
FROM employees
WHERE department = 'IT';
```

Filter first, aggregate later.

---

# Aggregate with Expression

```sql
SELECT SUM(salary * 12)
FROM employees;
```

---

# Using Alias

```sql
SELECT AVG(salary) AS avg_salary
FROM employees;
```

---

# Aggregates Ignore NULL

Example:

| salary |
| ------ |
| 50000  |
| NULL   |
| 70000  |

```sql
SELECT AVG(salary)
```

Result:

```text
(50000 + 70000) / 2
```

---

# Aggregate Without GROUP BY

Returns single row.

```sql
SELECT COUNT(*)
FROM employees;
```

---

# Aggregate With GROUP BY (Preview)

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

---

# Nested Aggregates (Not Allowed)

Wrong:

```sql
SELECT AVG(SUM(salary))
FROM employees;
```

Must use subquery.

---

# Aggregate with ORDER BY

```sql
SELECT MAX(salary)
FROM employees
ORDER BY salary;
```

ORDER BY useless here (single row).

---

# Common Interview Queries

Total employees:

```sql
SELECT COUNT(*)
FROM employees;
```

Highest salary:

```sql
SELECT MAX(salary)
FROM employees;
```

Average salary:

```sql
SELECT AVG(salary)
FROM employees;
```

---

# COUNT(*) vs COUNT(column)

COUNT(*)

* counts all rows

COUNT(column)

* ignores NULL values

---

# Aggregate with Condition

```sql
SELECT SUM(salary)
FROM employees
WHERE department = 'IT';
```

---

# Common Mistakes

Wrong:

```sql
SELECT name, COUNT(*)
FROM employees;
```

This requires GROUP BY.

---

Correct:

```sql
SELECT COUNT(*)
FROM employees;
```

---

# Performance Tip

COUNT(*) is optimized internally. Prefer it.

---

# Mental Model

Aggregate functions:

* Combine rows
* Return single value
* Ignore NULL
* Used with GROUP BY
