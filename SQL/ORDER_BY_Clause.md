# ORDER BY Clause

ORDER BY is used to **sort the result set**.

Basic syntax:

```sql
SELECT columns
FROM table
ORDER BY column;
```

---

# Default Sorting (Ascending)

```sql
SELECT *
FROM employees
ORDER BY salary;
```

Default is **ASC (ascending)**.

Equivalent to:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

---

# Descending Order

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

# Sorting by Multiple Columns

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

Meaning:

* First sort by department
* Then sort salary inside each department

---

# Example

Data:

| name | dept | salary |
| ---- | ---- | ------ |
| A    | IT   | 50000  |
| B    | IT   | 70000  |
| C    | HR   | 60000  |

Query:

```sql
SELECT *
FROM employees
ORDER BY dept, salary DESC;
```

Result:

```text
C HR 60000
B IT 70000
A IT 50000
```

---

# Sorting by Column Position

```sql
SELECT name, salary
FROM employees
ORDER BY 2 DESC;
```

This sorts by **second column (salary)**.

Not recommended in production (hard to read).

---

# Sorting by Alias

```sql
SELECT name, salary * 12 AS yearly
FROM employees
ORDER BY yearly DESC;
```

---

# ORDER BY with WHERE

```sql
SELECT *
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

Execution order:

* WHERE filter first
* Then sorting

---

# ORDER BY with Multiple Conditions

```sql
SELECT *
FROM employees
ORDER BY department ASC, name ASC;
```

---

# Sorting Strings

```sql
SELECT *
FROM employees
ORDER BY name;
```

Alphabetical sorting.

---

# Sorting Dates

```sql
SELECT *
FROM orders
ORDER BY order_date DESC;
```

Latest records first.

---

# Handling NULL Values

Default behavior:

* NULLs come first (DB dependent)

Force order:

(PostgreSQL)

```sql
SELECT *
FROM employees
ORDER BY salary DESC NULLS LAST;
```

---

# LIMIT Clause

LIMIT restricts number of rows.

```sql
SELECT *
FROM employees
LIMIT 5;
```

Returns first 5 rows.

---

# ORDER BY + LIMIT (Most Common Interview Pattern)

Top 3 highest salary:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

---

# Pagination

```sql
SELECT *
FROM employees
ORDER BY id
LIMIT 5 OFFSET 5;
```

Page 2 (skip first 5 rows).

---

# LIMIT Without ORDER BY (Danger)

```sql
SELECT *
FROM employees
LIMIT 5;
```

Result is unpredictable.

Always use ORDER BY with LIMIT.

---

# Top N Pattern

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

Highest salary.

---

# Bottom N Pattern

```sql
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 1;
```

Lowest salary.

---

# ORDER BY Expression

```sql
SELECT name, salary
FROM employees
ORDER BY salary * 12 DESC;
```

---

# Interview Patterns

Top N:

```sql
ORDER BY column DESC LIMIT N
```

Pagination:

```sql
LIMIT N OFFSET M
```

Sorting multiple:

```sql
ORDER BY col1, col2
```

---

# Common Mistakes

Wrong:

```sql
SELECT *
ORDER BY salary
FROM employees;
```

Correct:

```sql
SELECT *
FROM employees
ORDER BY salary;
```

---

Wrong:

```sql
SELECT *
FROM employees
LIMIT 5
ORDER BY salary;
```

Correct:

```sql
SELECT *
FROM employees
ORDER BY salary
LIMIT 5;
```

---

# Mental Model

ORDER BY:

* Sorts data
* Used after filtering
* Works with LIMIT
* Essential for Top N queries
