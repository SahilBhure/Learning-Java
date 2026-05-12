# Generics

Introduction

Generics provide compile-time type safety for classes and methods. They eliminate many casts and improve reusability.

Key concepts
- Generic class: class Box<T> { T value; }
- Bounded types: <T extends Number>
- Wildcards: ? extends T (producer), ? super T (consumer)

Example

```java
public static <T> void copy(List<T> src, List<T> dest) { dest.addAll(src); }
List<Integer> ints = List.of(1,2,3);
```

PECS mnemonic
- Producer Extends, Consumer Super: use ? extends when reading, ? super when writing.

TODO: add examples for generic methods, type erasure considerations, and common pitfalls.
