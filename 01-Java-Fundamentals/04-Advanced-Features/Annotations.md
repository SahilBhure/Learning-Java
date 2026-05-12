# Annotations

Overview

Annotations provide metadata and can be processed at compile-time or runtime.

Common built-ins
- @Override, @Deprecated, @SuppressWarnings, @FunctionalInterface

Custom annotations
- Define with @interface and specify @Retention and @Target.

Examples

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Timed { long value() default 0; }
```

Use-cases
- Validation frameworks (JSR-380), dependency injection (Spring), compile-time code generation (Lombok/AutoValue), and AOP instrumentation.
