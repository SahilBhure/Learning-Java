# Comparator and Comparable

Overview

Comparable (natural ordering) and Comparator (external, flexible ordering) are used to sort objects.

Comparable
- Implement Comparable<T> and define compareTo(T o) for natural order.

Comparator
- Use Comparator.comparing, reversed(), thenComparing(), or lambda expressions for ad-hoc ordering.

Example

```java
public class Person implements Comparable<Person> {
  private String name;
  private int age;
  public int compareTo(Person other) { return Integer.compare(this.age, other.age); }
}

Comparator<Person> byName = Comparator.comparing(Person::getName);
Collections.sort(list, byName);
```

Notes
- Use Comparator.nullsFirst/Last when nulls are possible.
- For performance, avoid expensive comparators in hot loops.

TODO: add examples for multi-field sorting and tie-breakers.
