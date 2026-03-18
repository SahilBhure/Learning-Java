
# 1. What is Two Pointers?

Two Pointers is a technique where you use **two indices (pointers)** to traverse an array or string.

---

### Instead of:

* Using nested loops (O(n²))

You use:

> Two pointers → often reduces to O(n)

---

# 2. Why Two Pointers is Important

* Reduces time complexity
* Avoids nested loops
* Used in MANY interview problems

---

### Real Insight

> If array is sorted → think Two Pointers first

---

# 3. Types of Two Pointer Approaches

---

## Type 1: Opposite Direction

* One pointer at start
* One at end

```text
left →         ← right
```

---

### Used in:

* Reverse array
* Pair sum in sorted array

---

## Type 2: Same Direction (Fast & Slow)

```text
slow → → →  
fast → → → → →
```

---

### Used in:

* Removing duplicates
* Sliding window (advanced)

---

# 4. Classic Problem: Two Sum (Sorted Array)

---

## Problem

Given sorted array, find two numbers that sum to target.

---

## Brute Force

O(n²)

---

## Optimal (Two Pointers)

---

### Logic

* If sum < target → move left forward
* If sum > target → move right backward
* If equal → found

---

### Code

```java id="f9m9zn"
int[] twoSum(int[] arr, int target) {
    int left = 0;
    int right = arr.length - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target) {
            return new int[]{left, right};
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return new int[]{};
}
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> “Use sorted property to eliminate search space”

---

# 5. Classic Problem: Reverse Array

---

### Already Seen

```java
while (left < right) {
    swap(arr[left], arr[right]);
    left++;
    right--;
}
```

---

### Pattern

> Opposite direction pointers

---

# 6. Fast & Slow Pointer (Very Important)

---

## Example: Remove Duplicates from Sorted Array

---

### Idea

* Slow pointer → place unique elements
* Fast pointer → scan array

---

### Code

```java id="ybbsye"
int removeDuplicates(int[] nums) {
    int slow = 0;

    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }

    return slow + 1;
}
```

---

### Pattern Learned

> “Overwrite duplicates using slow pointer”

---

# 7. When to Use Two Pointers

---

## Look for these signals:

* Sorted array
* Pair problems
* Palindrome problems
* In-place modifications
* Subarray / substring problems

---

# 8. Two Pointers vs Hashing

---

## Hashing

* Works on unsorted arrays
* Uses extra space

---

## Two Pointers

* Works on sorted arrays
* No extra space

---

### Trade-off

```text
Hashing → O(n) time, O(n) space  
Two Pointers → O(n) time, O(1) space
```

---

# 9. Common Mistakes

---

## 1. Using on Unsorted Array 

Two pointers requires:

> Sorted order (most cases)

---

## 2. Wrong Pointer Movement

Always ask:

* When do I move left?
* When do I move right?

---

## 3. Infinite Loop

Ensure:

```java
left < right
```

---

# 10. Mental Model

Think of two pointers as:

```text
Shrinking search space intelligently
```

---

# 11. Pattern Summary

---

## Opposite Direction

* Start & end
* Move inward

---

## Same Direction

* Fast scans
* Slow updates

---

# 12. Interview Thinking

When you see:

* Sorted array
* Pair sum
* Remove duplicates
* Reverse

 Immediately think:

> “Can I use Two Pointers?”

---

# 13. Key Takeaways

* Reduces O(n²) → O(n)
* Uses array properties
* No extra space
* Extremely common in interviews

---
