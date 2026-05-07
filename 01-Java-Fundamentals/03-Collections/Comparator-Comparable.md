# Comparator and Comparable

How to compare objects in Java using Comparable and Comparator.

Contents:
- Comparable interface
- Comparator interface
- Lambda comparators and method references

## Example

```java
Comparator<Person> byAge = Comparator.comparingInt(Person::getAge);
```

## TODO
- Add examples for sorting custom objects
