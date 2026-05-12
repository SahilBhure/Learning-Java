# Generics

Introduction

Generics provide compile-time type safety for classes and methods. They eliminate many casts and improve reusability.

Key concepts
- Generic class: class Box<T> { private T value; public T get() { return value; } }
- Bounded types: <T extends Number>
- Wildcards: ? extends T (producer), ? super T (consumer)

PECS mnemonic
- Producer Extends, Consumer Super: use ? extends when reading from a generic source, ? super when writing into it.

Examples

```java
public static <T> void copy(List<? extends T> src, List<? super T> dest) {
  for (T t : src) dest.add(t);
}

Box<Integer> b = new Box<>();
```

Type erasure and limitations
- Java generics are implemented via type erasure: runtime has no generic type parameters. You cannot create new T[] or use instanceof with parameterized types.

Common interview questions
- Explain type erasure and implications for instanceof and arrays.
- Why do we use wildcards and what do ? extends and ? super mean practically?
