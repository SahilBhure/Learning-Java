# Arrays and Strings

## Table of Contents
1. [Arrays](#arrays)
2. [Strings](#strings)
3. [Common Problems](#common-problems)

---

## Arrays

### What is an Array?
A fixed-size collection of elements of the same type.

### Declaration and Initialization
```java
// Declaration
int[] arr;
int arr[];

// Initialization with size
int[] arr = new int[5];  // Creates array of size 5 with default values (0)

// Initialization with values
int[] arr = {1, 2, 3, 4, 5};

// 2D Array
int[][] matrix = new int[3][3];
int[][] matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
```

### Accessing Elements
```java
int[] arr = {10, 20, 30, 40, 50};

System.out.println(arr[0]);   // 10
System.out.println(arr[2]);   // 30
System.out.println(arr.length);  // 5

// Iterate
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// Enhanced for loop
for (int num : arr) {
    System.out.println(num);
}
```

### Array Operations
```java
int[] arr = {3, 1, 4, 1, 5};

// Sort
Arrays.sort(arr);  // {1, 1, 3, 4, 5}

// Search (requires sorted array)
int index = Arrays.binarySearch(arr, 4);  // 3

// Fill
Arrays.fill(arr, 0);  // All elements become 0

// Copy
int[] copy = Arrays.copyOf(arr, arr.length);
int[] partial = Arrays.copyOfRange(arr, 0, 3);

// Convert to List
List<Integer> list = Arrays.asList(1, 2, 3);
```

### Common Array Problems

#### 1. Find Maximum
```java
public int findMax(int[] arr) {
    int max = arr[0];
    for (int i = 1; i < arr.length; i++) {
        max = Math.max(max, arr[i]);
    }
    return max;
}
```

#### 2. Reverse Array
```java
public void reverseArray(int[] arr) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}
```

#### 3. Check if Sorted
```java
public boolean isSorted(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i - 1]) {
            return false;
        }
    }
    return true;
}
```

---

## Strings

### What is a String?
A sequence of characters. Immutable in Java.

### Declaration
```java
// Literal (String pool)
String str1 = "Hello";
String str2 = "Hello";

// Object (Heap memory)
String str3 = new String("Hello");

str1 == str2;      // true (same reference in pool)
str1 == str3;      // false (different references)
str1.equals(str3); // true (same content)
```

### String Methods
```java
String str = "Hello World";

// Length
str.length();  // 11

// Character access
str.charAt(0);  // 'H'

// Substring
str.substring(0, 5);  // "Hello"
str.substring(6);     // "World"

// Case conversion
str.toUpperCase();  // "HELLO WORLD"
str.toLowerCase();  // "hello world"

// Search
str.indexOf('l');       // 2
str.lastIndexOf('l');   // 9
str.contains("World");  // true
str.startsWith("Hello"); // true
str.endsWith("World");   // true

// Replace
str.replace('l', 'x');  // "Hexxo Worxd"
str.replaceAll("World", "Java");  // "Hello Java"

// Trim
" Hello ".trim();  // "Hello"

// Split
String[] words = "Hello,World,Java".split(",");
// {"Hello", "World", "Java"}

// Compare
str.compareTo("Hello World");  // 0 (equal)
str.compareToIgnoreCase("hello world");  // 0
```

### String Immutability
```java
String str = "Hello";
str = str + " World";  // Creates new String object

// String is immutable, so modifying creates new object
String original = "Hello";
original.concat(" World");  // Returns new String
System.out.println(original);  // Still "Hello"
```

### StringBuilder and StringBuffer
```java
// For mutable strings, use StringBuilder (not thread-safe)
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
String result = sb.toString();  // "Hello World"

// For thread-safe mutable strings, use StringBuffer
StringBuffer sf = new StringBuffer();
sf.append("Hello");

// StringBuilder is faster (not synchronized)
// StringBuffer is thread-safe but slower
```

### Common String Problems

#### 1. Reverse String
```java
public String reverseString(String str) {
    return new StringBuilder(str).reverse().toString();
}
```

#### 2. Check Palindrome
```java
public boolean isPalindrome(String str) {
    String cleaned = str.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
    return cleaned.equals(new StringBuilder(cleaned).reverse().toString());
}
```

#### 3. Check Anagram
```java
public boolean isAnagram(String s1, String s2) {
    char[] arr1 = s1.replaceAll(" ", "").toCharArray();
    char[] arr2 = s2.replaceAll(" ", "").toCharArray();
    Arrays.sort(arr1);
    Arrays.sort(arr2);
    return Arrays.equals(arr1, arr2);
}
```

#### 4. First Non-Repeating Character
```java
public char firstNonRepeatChar(String str) {
    Map<Character, Integer> map = new LinkedHashMap<>();
    
    for (char c : str.toCharArray()) {
        map.put(c, map.getOrDefault(c, 0) + 1);
    }
    
    for (char c : str.toCharArray()) {
        if (map.get(c) == 1) {
            return c;
        }
    }
    return '\0';
}
```

#### 5. Count Vowels
```java
public int countVowels(String str) {
    int count = 0;
    String vowels = "aeiouAEIOU";
    for (char c : str.toCharArray()) {
        if (vowels.contains(String.valueOf(c))) {
            count++;
        }
    }
    return count;
}
```

---

## Common Problems

### Two Sum Problem
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
// Time: O(n), Space: O(n)
```

### Remove Duplicates
```java
public int removeDuplicates(int[] nums) {
    int k = 1;
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] != nums[i - 1]) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
}
// Time: O(n), Space: O(1)
```

### Rotate Array
```java
public void rotate(int[] nums, int k) {
    k = k % nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}

private void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
// Time: O(n), Space: O(1)
```

### Interview Questions

### Q1: What's the difference between == and equals() for Strings?
**Answer:** == compares references, equals() compares content.

### Q2: Why is String immutable?
**Answer:** For security, thread-safety, and caching in string pool.

### Q3: When to use StringBuilder vs StringBuffer?
**Answer:** StringBuilder for single-threaded (faster), StringBuffer for multi-threaded (thread-safe).
