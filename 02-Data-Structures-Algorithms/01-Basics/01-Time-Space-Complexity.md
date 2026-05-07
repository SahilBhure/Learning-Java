# Time and Space Complexity Analysis

## Table of Contents
1. [Big O Notation](#big-o-notation)
2. [Time Complexity](#time-complexity)
3. [Space Complexity](#space-complexity)
4. [Complexity Analysis Examples](#complexity-analysis-examples)

---

## Big O Notation

Big O notation describes how an algorithm's performance grows as input size increases.

### Common Big O Notations

| Notation | Name | Example |
|----------|------|----------|
| O(1) | Constant | Array access by index |
| O(log n) | Logarithmic | Binary Search |
| O(n) | Linear | Simple Loop |
| O(n log n) | Linearithmic | Merge Sort, Quick Sort |
| O(n²) | Quadratic | Nested Loops |
| O(n³) | Cubic | Triple Nested Loops |
| O(2^n) | Exponential | Recursive Fibonacci |
| O(n!) | Factorial | Permutations |

### Complexity Graph
```
        n!
       /
      / 2^n
     /
    / n³
   /
  / n² 
 /
/ n log n
/
/ n
/
/ log n
/_______ O(1)
```

### Ranking (from best to worst)
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2^n) < O(n!)
```

---

## Time Complexity

### O(1) - Constant Time
Time doesn't depend on input size.

```java
public int getFirstElement(int[] arr) {
    return arr[0];  // Always takes same time
}

public boolean isTrue() {
    return true;  // Constant operation
}
```

### O(log n) - Logarithmic Time
Time increases logarithmically with input size.

```java
// Binary Search
public int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

### O(n) - Linear Time
Time grows proportionally with input size.

```java
// Linear Search
public int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) return i;
    }
    return -1;  // Loop runs n times in worst case
}

// Finding max element
public int findMax(int[] arr) {
    int max = arr[0];
    for (int i = 1; i < arr.length; i++) {  // n-1 iterations
        max = Math.max(max, arr[i]);
    }
    return max;
}
```

### O(n log n) - Linearithmic Time
Combination of linear and logarithmic.

```java
// Merge Sort
public void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);           // O(log n) levels
        mergeSort(arr, mid + 1, right);      // O(log n) levels
        merge(arr, left, mid, right);        // O(n) per level
    }
}
// Total: O(n log n)
```

### O(n²) - Quadratic Time
Nested loops.

```java
// Bubble Sort
public void bubbleSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n; i++) {           // First loop: n times
        for (int j = 0; j < n - i - 1; j++) { // Second loop: n times
            if (arr[j] > arr[j + 1]) {
                // Swap
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
// Total: n * n = O(n²)
```

### O(2^n) - Exponential Time
Doubles with each increase in input.

```java
// Recursive Fibonacci (without memoization)
public int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
    // 2^n function calls
}
```

---

## Space Complexity

Analyzes how much extra memory an algorithm uses.

### O(1) - Constant Space
```java
public int sum(int[] arr) {
    int sum = 0;  // Only one extra variable
    for (int num : arr) {
        sum += num;
    }
    return sum;
}
```

### O(n) - Linear Space
```java
public int[] createArray(int n) {
    int[] result = new int[n];  // Creates array of size n
    return result;
}

// DFS uses call stack - O(h) where h is height
public void dfs(TreeNode node) {
    if (node == null) return;
    dfs(node.left);    // Stack space
    dfs(node.right);   // Stack space
}
```

### O(log n) - Logarithmic Space
```java
// Binary Search uses stack space proportional to log n
public int binarySearchRecursive(int[] arr, int target, int left, int right) {
    if (left > right) return -1;
    
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) 
        return binarySearchRecursive(arr, target, mid + 1, right);
    else 
        return binarySearchRecursive(arr, target, left, mid - 1);
}
// Recursion depth: log n
```

### O(n²) - Quadratic Space
```java
public int[][] createMatrix(int n) {
    int[][] matrix = new int[n][n];  // Creates n×n matrix
    return matrix;
}
```

---

## Complexity Analysis Examples

### Example 1: Two separate loops
```java
for (int i = 0; i < n; i++) {           // O(n)
    System.out.println(i);
}
for (int j = 0; j < n; j++) {           // O(n)
    System.out.println(j);
}
// Total: O(n) + O(n) = O(2n) = O(n)
```

### Example 2: Nested loops
```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + "," + j);
    }
}
// Total: O(n) * O(n) = O(n²)
```

### Example 3: Different sizes
```java
for (int i = 0; i < n; i++) {           // O(n)
    System.out.println(i);
}
for (int j = 0; j < m; j++) {           // O(m)
    System.out.println(j);
}
// Total: O(n + m)
```

### Example 4: Dependent loops
```java
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        System.out.println(i + "," + j);
    }
}
// Iterations: n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 = O(n²)
```

---

## Interview Questions

### Q1: What is time complexity?
**Answer:** Time complexity describes how the runtime of an algorithm grows with input size, measured in Big O notation.

### Q2: Rank these complexities from best to worst
O(n²), O(1), O(n), O(log n), O(2^n)

**Answer:** O(1) < O(log n) < O(n) < O(n²) < O(2^n)

### Q3: What's the time complexity of binary search?
**Answer:** O(log n) because it divides the search space in half each time.

### Q4: Why do we drop constants in Big O?
**Answer:** Because Big O shows growth rate. O(2n) becomes O(n) because the constant doesn't affect how algorithm scales.

### Q5: What's the difference between O(n) and O(2n)?
**Answer:** Theoretically no difference in Big O terms. Both are O(n). The constant is ignored as n grows large.
