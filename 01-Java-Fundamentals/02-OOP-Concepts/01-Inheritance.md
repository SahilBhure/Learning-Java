# Inheritance

## Table of Contents
1. [Introduction](#introduction)
2. [Types of Inheritance](#types-of-inheritance)
3. [super Keyword](#super-keyword)
4. [Method Overriding](#method-overriding)
5. [Best Practices](#best-practices)

---

## Introduction

### What is Inheritance?
Inheritance is a mechanism where a child class inherits properties and methods from a parent class.

### Syntax
```java
public class Parent {
    public void parentMethod() {
        System.out.println("Parent method");
    }
}

public class Child extends Parent {
    public void childMethod() {
        System.out.println("Child method");
    }
}

// Usage
Child child = new Child();
child.parentMethod();   // Available from parent
child.childMethod();    // Own method
```

### Benefits
- Code reusability
- Method overriding (runtime polymorphism)
- Code maintainability
- Hierarchical classification

---

## Types of Inheritance

### 1. Single Inheritance
Child inherits from one parent.

```java
public class Animal {
    public void eat() {
        System.out.println("Animal eating");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("Dog barking");
    }
}
```

### 2. Multi-level Inheritance
Chain of inheritance: Grandparent → Parent → Child

```java
public class Animal {
    public void eat() {
        System.out.println("Eating");
    }
}

public class Mammal extends Animal {
    public void walk() {
        System.out.println("Walking");
    }
}

public class Dog extends Mammal {
    public void bark() {
        System.out.println("Barking");
    }
}

// Dog has access to eat() and walk()
```

### 3. Hierarchical Inheritance
Multiple children inherit from one parent.

```java
public class Animal {
    public void eat() {
        System.out.println("Eating");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("Barking");
    }
}

public class Cat extends Animal {
    public void meow() {
        System.out.println("Meowing");
    }
}
```

### 4. Multiple Inheritance (via Interfaces)
Java doesn't support multiple inheritance with classes, but with interfaces.

```java
public interface Swimmer {
    void swim();
}

public interface Flyer {
    void fly();
}

public class Duck implements Swimmer, Flyer {
    @Override
    public void swim() {
        System.out.println("Duck swimming");
    }
    
    @Override
    public void fly() {
        System.out.println("Duck flying");
    }
}
```

---

## super Keyword

The `super` keyword is used to refer to the parent class.

### Calling Parent Method
```java
public class Parent {
    public void display() {
        System.out.println("Parent display");
    }
}

public class Child extends Parent {
    @Override
    public void display() {
        super.display();  // Call parent method
        System.out.println("Child display");
    }
}

// Output:
// Parent display
// Child display
```

### Calling Parent Constructor
```java
public class Parent {
    private String name;
    
    public Parent(String name) {
        this.name = name;
    }
}

public class Child extends Parent {
    private int age;
    
    public Child(String name, int age) {
        super(name);      // Call parent constructor
        this.age = age;
    }
}
```

### super with Variables
```java
public class Parent {
    protected String name = "Parent";
}

public class Child extends Parent {
    protected String name = "Child";
    
    public void display() {
        System.out.println(name);         // Child
        System.out.println(super.name);   // Parent
    }
}
```

---

## Method Overriding

### Rules for Overriding
1. Method name must be same
2. Parameters must be same
3. Return type must be same or subtype (covariant)
4. Access modifier must be same or more accessible
5. Cannot throw broader exceptions
6. Must use @Override annotation

### Example
```java
public class Parent {
    public void display() {
        System.out.println("Parent display");
    }
}

public class Child extends Parent {
    @Override
    public void display() {
        System.out.println("Child display");
    }
}

// Runtime polymorphism
Parent obj = new Child();
obj.display();  // Calls Child's display()
```

### Access Modifier Rules
```java
public class Parent {
    protected void method() {  // protected
        // ...
    }
}

public class Child extends Parent {
    @Override
    public void method() {  // Can be public (more accessible)
        // ...
    }
}
```

---

## Best Practices

### 1. Prefer Composition over Inheritance
```java
// Bad: Inheritance
public class Circle extends Shape {
    // Might inherit irrelevant methods
}

// Good: Composition
public class Circle {
    private Shape shape;
    
    public void draw() {
        shape.draw();
    }
}
```

### 2. Use Abstract Classes for Common Behavior
```java
public abstract class Animal {
    public abstract void makeSound();
    
    public void eat() {
        System.out.println("Animal eating");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }
}
```

### 3. Avoid Deep Hierarchies
```java
// Bad: Too deep
public class A {}
public class B extends A {}
public class C extends B {}
public class D extends C {}

// Good: Flatter structure
public interface Common {}
public class A implements Common {}
public class B implements Common {}
```

### 4. Use Interfaces for Multiple Inheritance
```java
public interface Serializable {}
public interface Cloneable {}

public class MyClass implements Serializable, Cloneable {
    // Implements both interfaces
}
```

---

## Interview Questions

### Q1: What's the difference between inheritance and composition?
**Answer:** Inheritance is "is-a" relationship, composition is "has-a" relationship. Composition is more flexible.

### Q2: Can you override a static method?
**Answer:** No, static methods are not overridden. They are hidden. Only instance methods can be overridden.

### Q3: Can you override a private method?
**Answer:** No, private methods are not visible to child class. They cannot be overridden.

### Q4: What happens if parent and child have same variable name?
**Answer:** Both variables exist separately. Use `super.variableName` to access parent's variable.

### Q5: Does Java support multiple inheritance?
**Answer:** No, Java doesn't support multiple inheritance with classes (to avoid diamond problem). Use interfaces instead.
