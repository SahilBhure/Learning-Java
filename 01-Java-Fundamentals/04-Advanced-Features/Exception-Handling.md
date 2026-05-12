# Exception Handling

Overview

Java exceptions are either checked (must be declared/handled) or unchecked (RuntimeException). Use try-with-resources for AutoCloseable resources.

Design guidelines
- Prefer meaningful checked exceptions for recoverable conditions and unchecked for programming errors.
- Wrap and translate low-level exceptions at boundaries of modules (e.g., DAO layer to service-layer exceptions).

Examples

```java
try (BufferedReader r = Files.newBufferedReader(path)) {
  return r.readLine();
} catch (IOException e) {
  throw new UncheckedIOException(e);
}
```

Anti-patterns
- Do not swallow exceptions (empty catch blocks).
- Avoid using exceptions for normal control flow.

Testing notes
- Use custom exception types to make behavior explicit and testable.
