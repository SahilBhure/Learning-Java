# Java Operators

## Table of Contents
1. [Arithmetic Operators](#arithmetic-operators)
2. [Relational Operators](#relational-operators)
3. [Logical Operators](#logical-operators)
4. [Bitwise Operators](#bitwise-operators)
5. [Assignment Operators](#assignment-operators)
6. [Ternary Operator](#ternary-operator)
7. [Operator Precedence](#operator-precedence)

---

## Arithmetic Operators

Used to perform mathematical operations.

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| + | Addition | 10 + 5 | 15 |
| - | Subtraction | 10 - 5 | 5 |
| * | Multiplication | 10 * 5 | 50 |
| / | Division | 10 / 5 | 2 |
| % | Modulus | 10 % 3 | 1 |
| ++ | Increment | i++ | i+1 |
| -- | Decrement | i-- | i-1 |

### Examples
```java
int a = 10, b = 5;

System.out.println(a + b);  // 15
System.out.println(a - b);  // 5
System.out.println(a * b);  // 50
System.out.println(a / b);  // 2
System.out.println(a % b);  // 0

// Pre and Post Increment
int x = 5;
System.out.println(++x);    // 6 (pre-increment)
System.out.println(x++);    // 6 (post-increment)
System.out.println(x);      // 7
```

---

## Relational Operators

Used to compare values. Return boolean (true/false).

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| == | Equal to | 5 == 5 | true |
| != | Not equal to | 5 != 3 | true |
| > | Greater than | 5 > 3 | true |
| < | Less than | 3 < 5 | true |
| >= | Greater than or equal | 5 >= 5 | true |
| <= | Less than or equal | 3 <= 5 | true |

### Examples
```java
int a = 5, b = 3;

System.out.println(a == b);  // false
System.out.println(a != b);  // true
System.out.println(a > b);   // true
System.out.println(a < b);   // false
System.out.println(a >= b);  // true
System.out.println(a <= b);  // false
```

---

## Logical Operators

Used to perform logical operations. Work with boolean values.

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| && | AND | true && false | false |
| \|\| | OR | true \|\| false | true |
| ! | NOT | !true | false |

### Truth Tables

#### AND (&&)
| A | B | A && B |
|---|---|--------|
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

#### OR (||)
| A | B | A \|\| B |
|---|---|----------|
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

#### NOT (!)
| A | !A |
|---|----|
| true | false |
| false | true |

### Examples
```java
int age = 25;
String status = "Active";

if (age >= 18 && status.equals("Active")) {
    System.out.println("User is eligible");
}

if (age < 18 || !status.equals("Active")) {
    System.out.println("Access denied");
}
```

### Short-Circuit Evaluation
```java
// && - stops if first condition is false
if (age < 18 && validateUser()) {  // validateUser() won't be called if age < 18 is false
    // ...
}

// || - stops if first condition is true
if (age >= 18 || validateUser()) {  // validateUser() won't be called if age >= 18 is true
    // ...
}
```

---

## Bitwise Operators

Operate on individual bits.

| Operator | Name | Example |
|----------|------|----------|
| & | AND | 5 & 3 = 1 |
| \| | OR | 5 \| 3 = 7 |
| ^ | XOR | 5 ^ 3 = 6 |
| ~ | NOT | ~5 = -6 |
| << | Left Shift | 5 << 1 = 10 |
| >> | Right Shift | 5 >> 1 = 2 |
| >>> | Unsigned Right Shift | 5 >>> 1 = 2 |

### Examples
```java
int a = 5;    // 0101
int b = 3;    // 0011

System.out.println(a & b);   // 1 (0001)
System.out.println(a | b);   // 7 (0111)
System.out.println(a ^ b);   // 6 (0110)
System.out.println(~a);      // -6

System.out.println(a << 1);  // 10 (multiply by 2)
System.out.println(a >> 1);  // 2 (divide by 2)
```

---

## Assignment Operators

Used to assign values to variables.

| Operator | Example | Equivalent |
|----------|---------|------------|
| = | a = 5 | a = 5 |
| += | a += 5 | a = a + 5 |
| -= | a -= 5 | a = a - 5 |
| *= | a *= 5 | a = a * 5 |
| /= | a /= 5 | a = a / 5 |
| %= | a %= 5 | a = a % 5 |
| &= | a &= 5 | a = a & 5 |
| \|= | a \|= 5 | a = a \| 5 |
| ^= | a ^= 5 | a = a ^ 5 |
| <<= | a <<= 5 | a = a << 5 |
| >>= | a >>= 5 | a = a >> 5 |
| >>>= | a >>>= 5 | a = a >>> 5 |

### Examples
```java
int a = 10;
a += 5;   // a = 15
a -= 3;   // a = 12
a *= 2;   // a = 24
a /= 4;   // a = 6
a %= 4;   // a = 2
```

---

## Ternary Operator

Conditional operator with three operands.

### Syntax
```java
condition ? value_if_true : value_if_false
```

### Examples
```java
int age = 25;
String status = (age >= 18) ? "Adult" : "Minor";
System.out.println(status);  // Adult

int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println(max);  // 20

// Nested ternary
int score = 75;
String grade = (score >= 90) ? "A" : (score >= 80) ? "B" : (score >= 70) ? "C" : "F";
System.out.println(grade);  // C
```

---

## Operator Precedence

Higher precedence = evaluated first

| Precedence | Operators |
|------------|----------|
| 1 (Highest) | () [] . |
| 2 | ++ -- + - ! ~ |
| 3 | * / % |
| 4 | + - |
| 5 | << >> >>> |
| 6 | < > <= >= instanceof |
| 7 | == != |
| 8 | & |
| 9 | ^ |
| 10 | \| |
| 11 | && |
| 12 | \|\| |
| 13 | ?: |
| 14 (Lowest) | = += -= *= /= |

### Example
```java
int result = 2 + 3 * 4;  // 14 (3*4 evaluated first)
int result2 = (2 + 3) * 4;  // 20 (parentheses first)
```

---

## Interview Questions

### Q1: What's the difference between == and equals()?
**Answer:** == compares references, equals() compares values. For strings, use equals().

### Q2: What's the difference between && and &?
**Answer:** && is logical AND with short-circuit, & is bitwise AND without short-circuit.

### Q3: Explain the difference between ++ and ++i?
**Answer:** i++ returns old value then increments, ++i increments then returns new value.

### Q4: What happens with bitwise AND between 5 and 3?
**Answer:** 5 (0101) & 3 (0011) = 1 (0001)
