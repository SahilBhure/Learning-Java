
# Problem 1: Maximum Sum Subarray of Size K

---

## Problem Statement

Given an array and integer `k`, find the **maximum sum of any subarray of size k**.

---

## Example

```text id="3b4tqv"
arr = [2,1,5,1,3,2], k = 3  
Output = 9  (subarray [5,1,3])
```

---

## Brute Force

---

### Idea

Check all subarrays of size k

---

### Code

```java id="dlv16u"
int maxSum = 0;

for (int i = 0; i <= arr.length - k; i++) {
    int sum = 0;
    for (int j = i; j < i + k; j++) {
        sum += arr[j];
    }
    maxSum = Math.max(maxSum, sum);
}
```

---

### Time Complexity

O(n * k)

---

## Optimal: Sliding Window

---

### Idea

* First window → calculate sum
* Slide window → add next, remove previous

---

### Code

```java id="o3uj1y"
int windowSum = 0;
int maxSum = 0;

// first window
for (int i = 0; i < k; i++) {
    windowSum += arr[i];
}
maxSum = windowSum;

// slide window
for (int i = k; i < arr.length; i++) {
    windowSum += arr[i];
    windowSum -= arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Fixed window → reuse previous computation

---

# Problem 2: Longest Substring Without Repeating Characters

---

## Problem Statement

Find the length of the longest substring without repeating characters.

---

## Example

```text id="egr0sc"
"abcabcbb" → 3
```

---

## Brute Force

---

### Idea

Check all substrings

---

### Complexity

O(n³)

---

## Optimal: Sliding Window + HashSet

---

### Code

```java id="v1a2w6"
Set<Character> set = new HashSet<>();
int left = 0, maxLen = 0;

for (int right = 0; right < s.length(); right++) {

    while (set.contains(s.charAt(right))) {
        set.remove(s.charAt(left));
        left++;
    }

    set.add(s.charAt(right));
    maxLen = Math.max(maxLen, right - left + 1);
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Expand → shrink until valid

---

# Problem 3: Longest Subarray with Sum ≤ K

---

## Problem Statement

Find the longest subarray with sum ≤ k

---

## Example

```text id="rmf3hr"
arr = [1,2,1,0,1,1,0], k = 4  
Output = 5
```

---

## Sliding Window Approach

---

### Code

```java id="o0odny"
int left = 0, sum = 0, maxLen = 0;

for (int right = 0; right < arr.length; right++) {
    sum += arr[right];

    while (sum > k) {
        sum -= arr[left];
        left++;
    }

    maxLen = Math.max(maxLen, right - left + 1);
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Maintain condition (sum ≤ k)

---

# Problem 4: Minimum Size Subarray Sum

---

## Problem Statement

Find smallest subarray with sum ≥ target

---

## Example

```text id="s02jco"
target = 7  
arr = [2,3,1,2,4,3]  
Output = 2  ([4,3])
```

---

## Sliding Window

---

### Code

```java id="mqyeu5"
int left = 0, sum = 0, minLen = Integer.MAX_VALUE;

for (int right = 0; right < arr.length; right++) {
    sum += arr[right];

    while (sum >= target) {
        minLen = Math.min(minLen, right - left + 1);
        sum -= arr[left];
        left++;
    }
}

return minLen == Integer.MAX_VALUE ? 0 : minLen;
```

---

### Pattern

> Shrink to find minimum

---

# Problem 5: Maximum Number of Vowels in Substring of Size K

---

## Problem Statement

Find max vowels in any substring of size k

---

## Example

```text id="hh3g11"
s = "abciiidef", k = 3 → 3
```

---

## Sliding Window

---

### Code

```java id="nb14sb"
int count = 0, maxCount = 0;

// first window
for (int i = 0; i < k; i++) {
    if (isVowel(s.charAt(i))) count++;
}
maxCount = count;

// slide window
for (int i = k; i < s.length(); i++) {
    if (isVowel(s.charAt(i))) count++;
    if (isVowel(s.charAt(i - k))) count--;

    maxCount = Math.max(maxCount, count);
}
```

---

### Pattern

> Fixed window + condition count

---

# Key Patterns Learned

---

## 1. Fixed Size Window

* Max sum subarray
* Vowel count

---

## 2. Variable Window

* Expand + shrink
* Maintain condition

---

## 3. Longest vs Smallest

* Longest → expand more
* Smallest → shrink aggressively

---

# Interview Signals

When you see:

* Subarray / substring
* Contiguous elements
* Max/min length
* Condition-based window

 Think:

> Sliding Window

---

# Practice Strategy

---

## You should:

* Dry run each problem
* Understand WHEN to shrink
* Understand WHAT condition is maintained

---

## Avoid:

* Memorizing code
* Ignoring condition logic

