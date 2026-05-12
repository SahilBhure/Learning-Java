# Annotations

Overview

Annotations provide metadata and can be processed at compile-time or runtime.

Common built-ins
- @Override, @Deprecated, @SuppressWarnings, @FunctionalInterface

Custom annotations
- Define with @interface and specify @Retention and @Target.

Example

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Timed { }
```

TODO: add examples for validation annotations, DI frameworks, and annotation processors.
