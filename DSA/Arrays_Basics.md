

## 1. What is an Array?

An array is a **linear data structure** that stores elements in **contiguous memory locations**.

---

### Key Properties

* Fixed size (in most languages like Java)
* Indexed (0-based indexing)
* Fast access using index

---

### Example

```java
int[] arr = {10, 20, 30, 40};
```

Memory representation:

```text
Index:   0    1    2    3
Value:  10   20   30   40
```

---

## 2. Why Arrays Matter

Arrays are the **foundation of DSA**.

Most problems are built on top of:

* Arrays
* Strings (which are arrays of characters)

---

### Real Interview Insight

> If you master arrays, you unlock ~40% of DSA problems

---

## 3. Time Complexity of Array Operations

| Operation       | Time Complexity |
| --------------- | --------------- |
| Access (arr[i]) | O(1)            |
| Search          | O(n)            |
| Insert (end)    | O(1)            |
| Insert (middle) | O(n)            |
| Delete          | O(n)            |

---

### Why Insert/Delete is O(n)?

Because elements must be **shifted**.

---

## 4. Types of Array Problems

You will encounter patterns like:

1. **Traversal**
2. **Searching**
3. **Modification**
4. **Subarrays**
5. **Pair-based problems (important)**
6. **Frequency counting (leads to Hashing)**

---

## 5. Basic Traversal (Must Know)

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

---

### Important Thinking

Whenever you see an array:

> First instinct = “Can I solve this by iterating once?”

---

## 6. Brute Force Thinking (VERY IMPORTANT)

Before jumping to optimal solutions:

> Always think brute force first

---

### Example Problem

Find max element in array.

---

### Brute Force (Correct thinking)

```java
int max = arr[0];

for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
```

---

### Time Complexity

O(n)

---

### Key Learning

> Not all brute force solutions are bad — some are already optimal

---

## 7. Common Mistakes Beginners Make

### 1. Ignoring Edge Cases

* Empty array
* Single element
* All elements same

---

### 2. Index Out of Bounds

```java
arr[i + 1] // risky if i is last index
```

---

### 3. Overcomplicating

Sometimes:

> Simple loop = correct answer

---

## 8. Important Patterns to Notice

Even at basics, start observing:

### Pattern 1: Full Traversal

* Check every element

---

### Pattern 2: Pair Comparison

```java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        // compare arr[i] and arr[j]
    }
}
```

Used in:

* Two Sum (brute force)
* Duplicate detection

---

### Pattern 3: Running Value

```java
sum += arr[i];
```

Used in:

* Prefix sums
* Subarray problems

---

## 9. Introduction to Subarrays

Subarray = **continuous part of array**

Example:

```text
[1, 2, 3]

Subarrays:
[1], [2], [3]
[1,2], [2,3]
[1,2,3]
```

---

### Total Subarrays Formula

```text
n * (n + 1) / 2
```

---

### Generating Subarrays (Brute Force)

```java
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        for (int k = i; k <= j; k++) {
            System.out.print(arr[k] + " ");
        }
        System.out.println();
    }
}
```

---

### Time Complexity

O(n³)

---

### Key Insight

> Many problems start with O(n³) brute force → optimized later

---

## 10. How to Approach Any Array Problem

Follow this order:

---

### Step 1: Understand Problem

* What is input?
* What is expected output?

---

### Step 2: Think Brute Force

* Try all possibilities
* Use nested loops if needed

---

### Step 3: Optimize

Ask:

* Can I reduce loops?
* Can I use extra space?
* Can I use a pattern?

---

## 11. Mental Model You Must Build

When you see an array:

Ask yourself:

* Can I solve in one pass?
* Do I need nested loops?
* Is this a pair problem?
* Can I store something while iterating?

---

## 12. Final Understanding

Arrays are not just storage.

They are:

* The base of almost all DSA problems
* The starting point of patterns like:

  * Hashing
  * Sliding Window
  * Two Pointers

