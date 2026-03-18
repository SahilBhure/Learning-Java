
# Problem 1: Two Sum II (Sorted Array)

---

## Problem Statement

Given a **sorted array**, find two numbers such that they add up to a target.

---

## Example

```text
Input: [2, 7, 11, 15], target = 9  
Output: [0, 1]
```

---

## Brute Force

---

### Code

```java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        if (arr[i] + arr[j] == target) {
            return new int[]{i, j};
        }
    }
}
```

---

### Time Complexity

O(n²)

---

## Optimal: Two Pointers

---

### Key Idea

Use sorted property:

* Smallest on left
* Largest on right

---

### Code

```java
int left = 0;
int right = arr.length - 1;

while (left < right) {
    int sum = arr[left] + arr[right];

    if (sum == target) return new int[]{left, right};
    else if (sum < target) left++;
    else right--;
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Shrinking search space using sorted array

---

# Problem 2: Container With Most Water

---

## Problem Statement

Given heights of vertical lines, find max water container.

---

## Example

```text
[1,8,6,2,5,4,8,3,7] → Output: 49
```

---

## Brute Force

Check all pairs:

```java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        int area = Math.min(height[i], height[j]) * (j - i);
        max = Math.max(max, area);
    }
}
```

---

### Time Complexity

O(n²)

---

## Optimal: Two Pointers

---

### Key Insight (VERY IMPORTANT)

Area depends on:

* Width = (right - left)
* Height = min(height[left], height[right])

---

### Strategy

* Move the **smaller height pointer**

---

### Code

```java
int left = 0, right = height.length - 1;
int max = 0;

while (left < right) {
    int area = Math.min(height[left], height[right]) * (right - left);
    max = Math.max(max, area);

    if (height[left] < height[right]) {
        left++;
    } else {
        right--;
    }
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Move the limiting factor

---

# Problem 3: Remove Duplicates from Sorted Array

---

## Problem Statement

Remove duplicates **in-place** and return new length.

---

## Example

```text
[1,1,2] → [1,2,_]
```

---

## Brute Force Idea

Use extra array (not optimal)

---

## Optimal: Fast & Slow Pointer

---

### Code

```java
int slow = 0;

for (int fast = 1; fast < nums.length; fast++) {
    if (nums[fast] != nums[slow]) {
        slow++;
        nums[slow] = nums[fast];
    }
}
return slow + 1;
```

---

### Time Complexity

O(n)

---

### Pattern

> Overwrite duplicates

---

# Problem 4: Valid Palindrome

---

## Problem Statement

Check if string is palindrome (ignore non-alphanumeric).

---

## Example

```text
"A man, a plan, a canal: Panama" → true
```

---

## Approach: Two Pointers

---

### Code

```java
int left = 0, right = s.length() - 1;

while (left < right) {
    while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
        left++;
    }
    while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
        right--;
    }

    if (Character.toLowerCase(s.charAt(left)) != 
        Character.toLowerCase(s.charAt(right))) {
        return false;
    }

    left++;
    right--;
}

return true;
```

---

### Pattern

> Skip + compare

---

# Problem 5: Squares of Sorted Array

---

## Problem Statement

Given sorted array (may have negatives), return sorted squares.

---

## Example

```text
[-4,-1,0,3,10] → [0,1,9,16,100]
```

---

## Brute Force

* Square all
* Sort → O(n log n)

---

## Optimal: Two Pointers

---

### Key Idea

Largest square comes from ends

---

### Code

```java
int n = nums.length;
int[] result = new int[n];

int left = 0, right = n - 1;
int index = n - 1;

while (left <= right) {
    int leftSq = nums[left] * nums[left];
    int rightSq = nums[right] * nums[right];

    if (leftSq > rightSq) {
        result[index--] = leftSq;
        left++;
    } else {
        result[index--] = rightSq;
        right--;
    }
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Fill result from end

---

# Key Patterns Learned

---

## 1. Opposite Pointer Movement

* Two Sum sorted
* Container problem

---

## 2. Move Smaller / Limiting Factor

* Container With Most Water

---

## 3. Fast & Slow Pointer

* Remove duplicates

---

## 4. Skip & Compare

* Palindrome

---

## 5. Build Result Backwards

* Squares problem

---

# Interview Signals

When you see:

* Sorted array → Two pointers
* Max/min pair → Opposite ends
* In-place modify → Fast & slow
* Palindrome → Compare ends

---

# Practice Advice

---

## Do this:

* Solve again without seeing
* Dry run each step
* Explain WHY pointer moves

---

## Avoid this:

* Memorizing code
* Skipping brute force thinking

