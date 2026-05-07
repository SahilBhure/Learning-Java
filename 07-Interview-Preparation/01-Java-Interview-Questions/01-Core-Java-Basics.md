# Core Java Interview Questions

## Table of Contents
1. [Basics](#basics)
2. [OOP Concepts](#oop-concepts)
3. [Memory Management](#memory-management)
4. [Collections](#collections)
5. [Advanced Questions](#advanced-questions)

---

## Basics

### Q1: What is Java?
**Answer:** Java is an object-oriented, platform-independent, secure, and multithreaded programming language. It follows the principle "Write Once, Run Anywhere" (WORA).

### Q2: What's the difference between JDK, JRE, and JVM?

| Component | Purpose | Contains |
|-----------|---------|----------|
| JVM | Executes bytecode | Runtime environment |
| JRE | Runs Java programs | JVM + libraries |
| JDK | Development kit | JRE + tools (compiler, debugger) |

### Q3: Explain the Java compilation process
```
.java file
   ↓
JavaC Compiler
   ↓
.class file (Bytecode)
   ↓
JVM (JIT Compiler)
   ↓
Machine Code (Platform-specific)
   ↓
Execution
```

### Q4: What are the main features of Java 8?
- Lambda expressions
- Streams API
- Functional interfaces
- Default methods in interfaces
- Method references
- Optional class

### Q5: What's the difference between pass by value and pass by reference?
**Answer:** Java is always pass by value. Primitives pass values, objects pass references (copy of reference, not object).

```java
public void modifyPrimitive(int x) {
    x = 10;  // Doesn't affect original
}

public void modifyObject(User user) {
    user.setName("John");  // Changes original object
    user = new User();     // Doesn't affect original reference
}
```

---

## OOP Concepts

### Q6: Explain the 4 pillars of OOP

#### 1. Encapsulation
Hiding internal details, exposing only necessary.

```java
public class User {
    private String name;  // Hidden
    private String email; // Hidden
    
    // Exposed through getters/setters
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;  // Can add validation
    }
}
```

#### 2. Inheritance
Child class inherits from parent class.

```java
public class Animal {
    public void eat() {
        System.out.println("Animal eating");
    }
}

public class Dog extends Animal {
    @Override
    public void eat() {
        System.out.println("Dog eating");
    }
}
```

#### 3. Polymorphism
Objects can take multiple forms.

```java
public interface Shape {
    void draw();
}

public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing circle");
    }
}

public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing square");
    }
}

// Usage
Shape shape = new Circle();
shape.draw();  // Draws circle

shape = new Square();
shape.draw();  // Draws square
```

#### 4. Abstraction
Showing only relevant details, hiding complexity.

```java
public abstract class Vehicle {
    abstract void start();
    
    public void stop() {
        System.out.println("Vehicle stopped");
    }
}

public class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car started");
    }
}
```

### Q7: What's the difference between abstract class and interface?

| Feature | Abstract Class | Interface |
|---------|---|---|
| Multiple inheritance | No | Yes |
| Constructor | Can have | Can't have |
| State | Can have | Can't have (Java 8+) |
| Access modifiers | public, private, protected | public only |
| Use case | "is-a" relationship | "can-do" capability |

### Q8: Explain method overloading and overriding

#### Overloading (Compile-time polymorphism)
Same method name, different parameters.

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

#### Overriding (Runtime polymorphism)
Child class provides implementation of parent method.

```java
public class Animal {
    public void eat() {
        System.out.println("Animal eating");
    }
}

public class Dog extends Animal {
    @Override
    public void eat() {
        System.out.println("Dog eating");
    }
}
```

---

## Memory Management

### Q9: Explain Java Memory Areas

```
┌─────────────────────────────────┐
│      JVM Memory                 │
├─────────────────────────────────┤
│  1. Heap                        │  (Shared by all threads)
│     - Objects                   │  (Garbage collected)
│                                 │
│  2. Stack                       │  (Each thread has own)
│     - Primitives                │  (Method calls)
│     - Object references         │  (Automatically freed)
│                                 │
│  3. Method Area                 │  (Shared by all)
│     - Class definitions         │  (Static content)
│     - Method code               │
│     - Constants                 │
│                                 │
│  4. Program Counter Register    │
│  5. Native Method Stack         │
└─────────────────────────────────┘
```

### Q10: What is garbage collection?
**Answer:** Automatic process that frees memory of objects no longer in use. JVM automatically manages this.

### Q11: What's the difference between == and equals()?

```java
String s1 = new String("Hello");
String s2 = new String("Hello");

s1 == s2;        // false (different references)
s1.equals(s2);   // true (same content)

// For custom objects
User u1 = new User(1, "John");
User u2 = new User(1, "John");

u1 == u2;        // false (different references)
u1.equals(u2);   // false (equals not overridden)

// Override equals() for proper comparison
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    User user = (User) o;
    return id == user.id && Objects.equals(name, user.name);
}
```

---

## Collections

### Q12: Explain Collection Hierarchy

```
Collection
├── List (Ordered, Duplicates allowed)
│   ├── ArrayList
│   ├── LinkedList
│   └── Vector
├── Set (Unique, No order)
│   ├── HashSet
│   ├── TreeSet
│   └── LinkedHashSet
└── Queue (FIFO)
    ├── PriorityQueue
    └── LinkedList

Map (Key-Value pairs)
├── HashMap
├── TreeMap
├── LinkedHashMap
└── ConcurrentHashMap
```

### Q13: When to use ArrayList vs LinkedList?

| Operation | ArrayList | LinkedList |
|-----------|-----------|------------|
| Access | O(1) - Fast | O(n) - Slow |
| Insert/Delete at start | O(n) - Slow | O(1) - Fast |
| Insert/Delete at end | O(1) - Fast | O(1) - Fast |
| Memory | Less | More |

### Q14: What's the difference between HashMap and Hashtable?

| Feature | HashMap | Hashtable |
|---------|---------|----------|
| Thread-safe | No | Yes |
| Null keys/values | Yes | No |
| Performance | Faster | Slower |
| Legacy | No | Yes (Legacy) |

---

## Advanced Questions

### Q15: What are generics and why use them?
**Answer:** Generics provide compile-time type checking and eliminate typecasting.

```java
// Without generics (unsafe)
List list = new ArrayList();
list.add("Hello");
list.add(123);
String str = (String) list.get(1);  // ClassCastException

// With generics (type-safe)
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123);  // Compile error
String str = list.get(0);  // No casting needed
```

### Q16: Explain Lambda expressions
**Answer:** Anonymous function providing concise syntax for functional programming.

```java
// Traditional
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
for (Integer num : numbers) {
    System.out.println(num);
}

// Lambda
numbers.forEach(num -> System.out.println(num));

// With Stream
numbers.stream()
    .filter(n -> n > 2)
    .map(n -> n * 2)
    .forEach(System.out::println);
```

### Q17: What are Streams?
**Answer:** Streams provide functional-style operations on collections.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

int sum = numbers.stream()
    .filter(n -> n > 2)      // Intermediate operation
    .map(n -> n * 2)         // Intermediate operation
    .reduce(0, Integer::sum);  // Terminal operation

System.out.println(sum);  // (3*2) + (4*2) + (5*2) = 24
```

### Q18: What's the Optional class?
**Answer:** Container for potentially null values, helping avoid NullPointerException.

```java
Optional<String> optional = Optional.ofNullable(name);

// Old way
if (name != null) {
    System.out.println(name);
}

// With Optional
optional.ifPresent(System.out::println);
optional.ifPresentOrElse(
    System.out::println,
    () -> System.out.println("Name not provided")
);

String result = optional.orElse("Unknown");
```
