# Streams & Lambda

Overview

Streams and lambdas support a functional style of programming for collections processing.

Common operations
- intermediate: map, filter, flatMap
- terminal: collect, reduce, forEach

Examples

```java
List<String> names = users.stream()
  .map(User::getName)
  .filter(n -> !n.isBlank())
  .collect(Collectors.toList());

Map<String, Long> counts = users.stream()
  .collect(Collectors.groupingBy(User::getCountry, Collectors.counting()));
```

Collectors and performance
- Use Collectors.toList() to collect results. For large datasets consider streaming with parallelStream but measure thread-safety and ordering effects.
