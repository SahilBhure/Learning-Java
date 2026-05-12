# Comparator and Comparable

Overview

Comparable (natural ordering) and Comparator (external, flexible ordering) are used to sort objects.

Comparable
- Implement Comparable<T> and define compareTo(T o) for natural order.

Comparator
- Use Comparator.comparing, reversed(), thenComparing(), or lambda expressions for ad-hoc ordering.

Examples

```java
public class Person implements Comparable<Person> {
  private final String name;
  private final int age;
  public Person(String name, int age){ this.name = name; this.age = age; }
  public int compareTo(Person other) { return Integer.compare(this.age, other.age); }
  public String getName(){ return name; }
}

Comparator<Person> byName = Comparator.comparing(Person::getName);
List<Person> people = List.of(new Person("A",20), new Person("B",18));
people.stream().sorted(byName).forEach(p -> System.out.println(p.getName()));
```

Multi-field sorting and null handling
- Use Comparator.nullsFirst/Last and thenComparing for tie-breakers.

```java
Comparator<Person> cmp = Comparator.comparing(Person::getAge)
                                   .thenComparing(Person::getName);
```

Performance notes
- Avoid expensive comparators in hot loops; precompute keys where possible.
