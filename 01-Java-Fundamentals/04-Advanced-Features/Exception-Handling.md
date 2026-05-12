# Exception Handling

Overview

Java exceptions are either checked (must be declared/handled) or unchecked (RuntimeException). Use try-with-resources for AutoCloseable resources.

Best practices
- Prefer meaningful custom exceptions when appropriate.
- Avoid using exceptions for flow control.
- Clean up resources using try-with-resources.

Example

```java
try (BufferedReader r = Files.newBufferedReader(path)) {
  return r.readLine();
} catch (IOException e) {
  throw new UncheckedIOException(e);
}
```

TODO: add patterns for API design and exception translation.
