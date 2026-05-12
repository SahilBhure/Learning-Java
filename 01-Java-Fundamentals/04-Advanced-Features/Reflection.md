# Reflection

Overview

Reflection enables inspecting and manipulating classes, methods, and fields at runtime. Useful for frameworks (serialization, DI), but has performance and security costs.

Examples

```java
Class<?> c = Class.forName("java.lang.String");
Method m = c.getMethod("substring", int.class);
String s = (String) m.invoke("hello", 1);
```

Use-cases and cautions
- Use reflection in libraries/frameworks; avoid frequent use in hot loops.
- Reflection can break encapsulation; prefer documented APIs.
