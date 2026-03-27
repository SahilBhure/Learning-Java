# WHERE Clause Deep Dive

The WHERE clause is used to **filter rows**.

Basic syntax:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

---

# Basic Comparison Operators

| Operator | Meaning               |
| -------- | --------------------- |
| =        | Equal                 |
| != or <> | Not equal             |
| >        | Greater than          |
| <        | Less than             |
| >=       | Greater than or equal |
| <=       | Less than or equal    |

---

# Examples

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

---

# Multiple Conditions (AND)

Both conditions must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT' AND salary > 50000;
```

---

# Multiple Conditions (OR)

At least one condition must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT' OR department = 'HR';
```

---

# NOT Operator

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

---

# BETWEEN

Used for range filtering.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 70000;
```

Equivalent to:

```sql
WHERE salary >= 40000 AND salary <= 70000;
```

---

# IN Operator

Used for multiple values.

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

Better than multiple OR conditions.

---

# NOT IN

```sql
SELECT *
FROM employees
WHERE department NOT IN ('HR');
```

---

# LIKE Operator (Pattern Matching)

Used for string pattern search.

| Pattern | Meaning                  |
| ------- | ------------------------ |
| %       | Any number of characters |
| _       | Single character         |

---

# LIKE Examples

Starts with:

```sql
SELECT *
FROM employees
WHERE name LIKE 'S%';
```

Ends with:

```sql
SELECT *
FROM employees
WHERE name LIKE '%l';
```

Contains:

```sql
SELECT *
FROM employees
WHERE name LIKE '%ah%';
```

Single character:

```sql
SELECT *
FROM employees
WHERE name LIKE 'S_';
```

---

# IS NULL

Used to check NULL values.

```sql
SELECT *
FROM employees
WHERE salary IS NULL;
```

---

# IS NOT NULL

```sql
SELECT *
FROM employees
WHERE salary IS NOT NULL;
```

---

# Combining Conditions

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000
AND name LIKE 'S%';
```

---

# Operator Precedence (Important)

Order:

1. NOT
2. AND
3. OR

Example:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR'
AND salary > 50000;
```

This executes as:

```sql
department = 'IT'
OR (department = 'HR' AND salary > 50000)
```

To avoid confusion, use parentheses:

```sql
SELECT *
FROM employees
WHERE (department = 'IT' OR department = 'HR')
AND salary > 50000;
```

---

# Filtering Numbers

```sql
SELECT *
FROM employees
WHERE salary >= 60000;
```

---

# Filtering Strings

```sql
SELECT *
FROM employees
WHERE name = 'Sahil';
```

---

# Filtering Dates

```sql
SELECT *
FROM orders
WHERE order_date > '2024-01-01';
```

---

# WHERE with Expressions

```sql
SELECT *
FROM employees
WHERE salary * 12 > 600000;
```

---

# Common Mistakes

Wrong:

```sql
SELECT *
FROM employees
WHERE salary = NULL;
```

Correct:

```sql
WHERE salary IS NULL;
```

---

Wrong:

```sql
WHERE department = "IT"
```

Correct:

```sql
WHERE department = 'IT'
```

---

# Performance Tip

Filtering early improves performance.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Better than filtering in application code.

---

# Mental Model

WHERE is used to:

* Filter rows
* Apply conditions
* Combine logic
* Reduce dataset size
