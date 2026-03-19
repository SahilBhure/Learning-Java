
# Problem 1: Binary Search (Classic)

---

## Problem Statement

Search a target in a sorted array.

---

## Example

```text id="l2x9af"
arr = [1,2,3,4,5], target = 4 → Output: 3
```

---

## Code

```java id="f2p1vz"
int binarySearch(int[] arr, int target) {
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

---

### Pattern

> Divide search space

---

# Problem 2: First and Last Position of Element

---

## Problem Statement

Find first and last occurrence of a target.

---

## Example

```text id="h6m03a"
arr = [5,7,7,8,8,10], target = 8  
Output = [3,4]
```

---

## Approach

Use binary search twice:

* Once for first occurrence
* Once for last occurrence

---

### Code (First Occurrence)

```java id="85y55j"
int firstOccurrence(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    int result = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            result = mid;
            right = mid - 1; // move left
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return result;
}
```

---

### Code (Last Occurrence)

```java id="ux0k7d"
int lastOccurrence(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    int result = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            result = mid;
            left = mid + 1; // move right
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return result;
}
```

---

### Pattern

> Keep searching even after finding target

---

# Problem 3: Search in Rotated Sorted Array

---

## Problem Statement

Array is sorted but rotated.

---

## Example

```text id="0dl4q7"
[4,5,6,7,0,1,2], target = 0 → Output = 4
```

---

## Key Insight

At least one half is always sorted

---

## Code

```java id="98s1ie"
int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) return mid;

        if (nums[left] <= nums[mid]) { // left sorted
            if (target >= nums[left] && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else { // right sorted
            if (target > nums[mid] && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }

    return -1;
}
```

---

### Pattern

> Identify sorted half

---

# Problem 4: Find Peak Element

---

## Problem Statement

Find element greater than neighbors.

---

## Example

```text id="r5a6u0"
[1,2,3,1] → Output: 2 (index)
```

---

## Insight

If mid < next → peak on right
Else → peak on left

---

## Code

```java id="59yzpl"
int findPeak(int[] nums) {
    int left = 0, right = nums.length - 1;

    while (left < right) {
        int mid = (left + right) / 2;

        if (nums[mid] < nums[mid + 1]) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    return left;
}
```

---

### Pattern

> Move toward increasing slope

---

# Problem 5: Binary Search on Answer (Minimum Eating Speed)

---

## Problem Statement

Find minimum speed to finish tasks within time.

---

## Example Idea

* Koko eating bananas
* Min speed needed

---

## Key Idea

Search answer range

---

## Code

```java id="8fsrhv"
int minSpeed(int[] piles, int h) {
    int left = 1;
    int right = Arrays.stream(piles).max().getAsInt();

    while (left < right) {
        int mid = (left + right) / 2;

        if (canFinish(piles, h, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

---

### Helper

```java id="zzn9bg"
boolean canFinish(int[] piles, int h, int speed) {
    int time = 0;

    for (int pile : piles) {
        time += Math.ceil((double)pile / speed);
    }

    return time <= h;
}
```

---

### Pattern

> Search answer, validate using function

---

# Key Patterns Learned

---

## 1. Classic Binary Search

* Find element

---

## 2. Bound Search

* First / Last occurrence

---

## 3. Modified Binary Search

* Rotated array
* Peak finding

---

## 4. Binary Search on Answer

* Guess answer
* Validate

---

# Interview Signals

When you see:

* Sorted array
* Rotated array
* Minimum / maximum value
* “Find best possible answer”

Think:

> Binary Search

---

# Practice Advice

---

## You must:

* Understand WHY pointer moves
* Not memorize conditions blindly
* Dry run carefully

---

## Avoid:

* Copying code
* Ignoring edge cases

