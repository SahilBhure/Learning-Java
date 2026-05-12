# Memory Management (Interview Notes)

Expanded notes

Java Memory Model: stack (primitive locals, references), heap (objects), metaspace (class metadata). GC overview: generational collectors (young/old), stop-the-world pauses, and ergonomics.

Common interview topics
- Explain minor vs major GC, GC logs interpretation, and how allocation patterns affect GC pressure.

Example: reduce GC churn by using object pools cautiously only when profiling shows allocation hotspots.
