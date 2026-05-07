# Variables and Data Types

## Table of Contents
1. [Variables](#variables)
2. [Data Types](#data-types)
3. [Type Casting](#type-casting)
4. [Best Practices](#best-practices)

---

## Variables

### What is a Variable?
A variable is a named memory location that stores a value. It's a container for data.

### Variable Declaration
```java
dataType variableName;
```

### Variable Initialization
```java
int age = 25;
String name = "John";
double salary = 50000.50;
```

### Variable Types

#### 1. Instance Variables (Non-static)
```java
public class Student {
    int age;           // Instance variable
    String name;       // Instance variable
    
    public void display() {
        System.out.println(name + " - " + age);
    }
}
```

#### 2. Class Variables (Static)
```java
public class Student {
    static int totalStudents = 0;  // Class variable
    
    public Student() {
        totalStudents++;
    }
}
```

#### 3. Local Variables
```java
public void method() {
    int localVar = 10;  // Local variable (scope limited to method)
}
```

---

## Data Types

### Primitive Data Types

| Type | Size | Range | Default Value |
|------|------|-------|---------------|
| byte | 1 byte | -128 to 127 | 0 |
| short | 2 bytes | -32,768 to 32,767 | 0 |
| int | 4 bytes | -2^31 to 2^31-1 | 0 |
| long | 8 bytes | -2^63 to 2^63-1 | 0L |
| float | 4 bytes | ~±3.4 × 10^38 | 0.0f |
| double | 8 bytes | ~±1.7 × 10^308 | 0.0d |
| char | 2 bytes | 0 to 65535 | '\u0000' |
| boolean | 1 bit | true/false | false |

### Examples
```java
byte b = 10;
short s = 1000;
int i = 100000;
long l = 10000000000L;

float f = 3.14f;
double d = 3.14159;

char c = 'A';
boolean flag = true;
```

### Non-Primitive Data Types

#### String
```java
String str = "Hello, World!";
String str2 = new String("Hello");
```

#### Arrays
```java
int[] arr = new int[5];
int[] arr2 = {1, 2, 3, 4, 5};
```

#### Objects/Classes
```java
String name = new String("John");
Student student = new Student();
```

---

## Type Casting

### Widening (Implicit) Casting
Automatic conversion from smaller to larger type.

```java
int num = 100;
long longNum = num;              // int -> long
float floatNum = longNum;        // long -> float
double doubleNum = floatNum;     // float -> double

// Order: byte -> short -> int -> long -> float -> double
```

### Narrowing (Explicit) Casting
Manual conversion from larger to smaller type (may lose data).

```java
double d = 10.5;
int num = (int) d;               // double -> int (loses decimal part)
long l = (long) d;
byte b = (byte) l;
```

### Example
```java
public class TypeCasting {
    public static void main(String[] args) {
        // Widening
        int intVal = 100;
        double doubleVal = intVal;  // Implicit
        System.out.println(doubleVal);  // 100.0
        
        // Narrowing
        double d = 95.5;
        int intVal2 = (int) d;  // Explicit
        System.out.println(intVal2);  // 95 (loses decimal)
    }
}
```

---

## Best Practices

### 1. Use Appropriate Data Types
```java
// Good
int age = 25;
boolean isActive = true;

// Bad
String age = "25";  // Should be int
int isActive = 1;   // Should be boolean
```

### 2. Use Constants
```java
public static final int MAX_SIZE = 100;
public static final String APP_NAME = "MyApp";
```

### 3. Meaningful Variable Names
```java
// Good
int numberOfStudents = 50;
String customerEmail = "customer@example.com";

// Bad
int n = 50;
String ce = "customer@example.com";
```

### 4. Initialize Variables
```java
// Good
int count = 0;
String message = "";

// Avoid uninitialized variables (for local variables)
int value;  // Uninitialized
```

### 5. Be Careful with Long and Float
```java
long bigNumber = 10000000000L;  // L suffix for long
float pi = 3.14f;               // f suffix for float
```

---

## Interview Questions

### Q1: What's the difference between int and long?
**Answer:** int is 4 bytes (range: -2^31 to 2^31-1), while long is 8 bytes (range: -2^63 to 2^63-1). Use long for larger numbers.

### Q2: What happens during implicit casting?
**Answer:** No data loss occurs as smaller types are converted to larger types that can accommodate all values.

### Q3: What's the difference between float and double?
**Answer:** float is 4 bytes (single precision), double is 8 bytes (double precision). Double is preferred for most calculations due to better precision.

### Q4: Can you cast from double to int?
**Answer:** Yes, using explicit casting: `int num = (int) 10.5;` But this loses the decimal part (10).

---

## Summary
- Variables store data in named memory locations
- Primitive types are basic (int, double, boolean, etc.)
- Non-primitive types are objects (String, Arrays, Classes)
- Implicit casting is automatic for wider types
- Explicit casting is needed for narrower types
- Use meaningful variable names and appropriate data types
