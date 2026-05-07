# Control Flow Statements

## Table of Contents
1. [if-else](#if-else)
2. [switch](#switch)
3. [Loops](#loops)
4. [Jump Statements](#jump-statements)

---

## if-else

### Simple if
```java
if (condition) {
    // code to execute if condition is true
}
```

### if-else
```java
if (condition) {
    // code if condition is true
} else {
    // code if condition is false
}
```

### if-else-if
```java
if (age < 13) {
    System.out.println("Child");
} else if (age < 18) {
    System.out.println("Teenager");
} else if (age < 60) {
    System.out.println("Adult");
} else {
    System.out.println("Senior");
}
```

### Nested if
```java
if (age >= 18) {
    if (salary > 50000) {
        System.out.println("Eligible for loan");
    }
}
```

---

## switch

### Traditional switch
```java
int day = 3;
switch(day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

### Switch with String (Java 7+)
```java
String fruit = "Apple";
switch(fruit) {
    case "Apple":
        System.out.println("Red fruit");
        break;
    case "Banana":
        System.out.println("Yellow fruit");
        break;
    default:
        System.out.println("Unknown fruit");
}
```

### Switch Expression (Java 12+)
```java
int result = switch(day) {
    case 1 -> 100;
    case 2 -> 200;
    case 3 -> 300;
    default -> 0;
};
```

### Fall-through Example
```java
int day = 6;
switch(day) {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        System.out.println("Weekday");
        break;
    case 6:
    case 7:
        System.out.println("Weekend");
        break;
}
```

---

## Loops

### for Loop
```java
// Traditional for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// Infinite loop
for (;;) {
    System.out.println("Infinite");
    break;  // Need break to exit
}
```

### Enhanced for Loop (for-each)
```java
int[] arr = {1, 2, 3, 4, 5};
for (int num : arr) {
    System.out.println(num);
}

// With collections
List<String> names = Arrays.asList("John", "Jane", "Bob");
for (String name : names) {
    System.out.println(name);
}
```

### while Loop
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

### do-while Loop
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
// Executes at least once even if condition is false
```

### Nested Loops
```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        System.out.print(i + " " + j + " ");
    }
    System.out.println();
}
```

---

## Jump Statements

### break
Terminates the innermost loop or switch.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Exits the loop
    }
    System.out.println(i);  // Prints 0-4
}

// Labeled break
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;  // Exits outer loop
        }
    }
}
```

### continue
Skips the current iteration.

```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    System.out.println(i);  // Prints odd numbers
}

// Labeled continue
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) {
            continue outer;  // Continue outer loop
        }
    }
}
```

### return
Exits the method.

```java
public int findValue(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;  // Exit method, return value
        }
    }
    return -1;  // Not found
}
```

---

## Best Practices

### 1. Use Enhanced for Loop When Possible
```java
// Good
for (int num : numbers) {
    System.out.println(num);
}

// Less readable
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

### 2. Prefer if-else for Multiple Conditions
```java
// Good for multiple unrelated conditions
if (age < 13) {
    type = "Child";
} else if (age < 18) {
    type = "Teen";
} else {
    type = "Adult";
}

// Use switch for single variable with multiple values
switch(day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
}
```

### 3. Avoid Infinite Loops Without Purpose
```java
// Good
while (condition) {
    // do something
}

// Avoid
while (true) {
    // something
}
```

---

## Interview Questions

### Q1: What's the difference between break and continue?
**Answer:** break exits the loop entirely, continue skips the current iteration and goes to the next.

### Q2: Can you use switch with String?
**Answer:** Yes, since Java 7. Switch works with String, Enum, and wrapper types.

### Q3: Difference between while and do-while?
**Answer:** do-while executes at least once before checking condition. while checks condition first.

### Q4: What's the difference between for and enhanced for loop?
**Answer:** Enhanced for is simpler for iterating but doesn't have index access. Use when you don't need index.
