# Stacks

Overview

Stacks follow LIFO and are used for expression evaluation, recursive simulation, and backtracking.

Solved example: Valid parentheses
```java
boolean isValid(String s) {
  Deque<Character> st = new ArrayDeque<>();
  for (char c : s.toCharArray()) {
    if (c == '(') st.push(')');
    else if (c == '{') st.push('}');
    else if (c == '[') st.push(']');
    else if (st.isEmpty() || st.pop() != c) return false;
  }
  return st.isEmpty();
}
```

Use ArrayDeque for performance and predictable behavior.
