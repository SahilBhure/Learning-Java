# Streams & Lambda

Overview

Streams and lambdas support a functional style of programming and make collection processing concise and expressive.

Common operations
- intermediate: map, filter, flatMap
- terminal: collect, forEach, reduce

Example

```java
List<String> names = users.stream()
  .map(User::getName)
  .filter(n -> !n.isEmpty())
  .collect(Collectors.toList());
```

Parallel streams
- Provide easy parallelism but watch for thread-safety and ordering concerns.

TODO: add collectors examples and performance tips.
