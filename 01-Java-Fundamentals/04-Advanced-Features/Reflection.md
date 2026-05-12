# Reflection

Overview

Reflection enables inspecting and manipulating classes, methods, and fields at runtime. Useful for frameworks (serialization, DI), but has performance and security costs.

Common APIs
- Class.forName, Class.getDeclaredMethods, Method.invoke, Field.setAccessible(true)

Example

```java
Class<?> c = Class.forName("com.example.Person");
Method m = c.getMethod("getName");
Object name = m.invoke(instance);
```

Notes
- Avoid excessive reflection in performance-sensitive code.
- Respect security manager policies and avoid breaking encapsulation without good reason.

TODO: add serialization/DIs examples.
