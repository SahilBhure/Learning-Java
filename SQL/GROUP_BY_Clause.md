# GROUP BY

GROUP BY is used to **group rows that have same values** into summary rows.

It is mainly used with **aggregate functions**.

---

# Basic Syntax

```sql
SELECT column, AGGREGATE_FUNCTION(column)
FROM table
GROUP BY column;
```

---

# Example Table

| name | department | salary |
| ---- | ---------- | ------ |
| A    | IT         | 50000  |
| B    | IT         | 70000  |
| C    | HR         | 60000  |
| D    | HR         | 55000  |

---

# Count Employees Per Department

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

Result:

```text
IT  2
HR  2
```

---

# Sum of Salary Per Department

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

---

# Average Salary Per Department

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

---

# Multiple Aggregates

```sql
SELECT 
    department,
    COUNT(*),
    AVG(salary),
    MAX(salary)
FROM employees
GROUP BY department;
```

---

# GROUP BY Multiple Columns

```sql
SELECT department, name, COUNT(*)
FROM employees
GROUP BY department, name;
```

Groups based on **combination**.

---

# Important Rule (Very Important)

Every column in SELECT must be:

* Either in GROUP BY
* Or inside aggregate function

Wrong:

```sql
SELECT department, name, COUNT(*)
FROM employees
GROUP BY department;
```

Correct:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

---

# WHERE vs GROUP BY

Execution order:

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

WHERE filters **before grouping**.

---

# Example

```sql
SELECT department, COUNT(*)
FROM employees
WHERE salary > 50000
GROUP BY department;
```

Steps:

* Filter salary > 50000
* Then group

---

# HAVING Clause

HAVING filters **after GROUP BY**.

Used with aggregates.

---

# Syntax

```sql
SELECT column, AGG(column)
FROM table
GROUP BY column
HAVING condition;
```

---

# Example: Departments With More Than 1 Employee

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```

---

# WHERE vs HAVING

WHERE:

* Filters rows

HAVING:

* Filters grouped results

---

# Example Comparison

Wrong:

```sql
SELECT department, COUNT(*)
FROM employees
WHERE COUNT(*) > 1
GROUP BY department;
```

Correct:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```

---

# GROUP BY + HAVING + ORDER BY

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 55000
ORDER BY avg_salary DESC;
```

---

# Multiple Conditions in HAVING

```sql
SELECT department, COUNT(*), AVG(salary)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2 AND AVG(salary) > 50000;
```

---

# GROUP BY With Expressions

```sql
SELECT department, SUM(salary * 12)
FROM employees
GROUP BY department;
```

---

# Most Asked Interview Patterns

Count per group:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

Max per group:

```sql
SELECT department, MAX(salary)
FROM employees
GROUP BY department;
```

Filter groups:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```

---

# Common Mistakes

Wrong:

```sql
SELECT department, salary
FROM employees
GROUP BY department;
```

Correct:

```sql
SELECT department, MAX(salary)
FROM employees
GROUP BY department;
```

---

# Mental Model

GROUP BY:

* Groups rows
* Used with aggregates
* HAVING filters groups
* WHERE filters rows
