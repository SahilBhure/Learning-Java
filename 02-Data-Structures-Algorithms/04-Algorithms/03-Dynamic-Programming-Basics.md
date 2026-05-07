# Dynamic Programming Basics

## Table of Contents
1. [What is DP?](#what-is-dp)
2. [Key Concepts](#key-concepts)
3. [Approaches](#approaches)
4. [Common Problems](#common-problems)

---

## What is DP?

Dynamic Programming is an optimization technique that solves complex problems by breaking them into overlapping subproblems and storing results to avoid redundant calculations.

### Characteristics
1. **Overlapping Subproblems** - Same problem solved multiple times
2. **Optimal Substructure** - Optimal solution contains optimal solutions to subproblems
3. **Memoization** - Caching intermediate results

### When to Use DP
- Problems with optimal substructure
- Overlapping subproblems exist
- Recursive solution is inefficient

---

## Key Concepts

### State
A unique configuration of a subproblem.

```
Fibonacci: State = position n
Coin Change: State = amount required
Knapsack: State = (item index, current weight)
```

### Recurrence Relation
How to calculate current state from previous states.

```
Fib(n) = Fib(n-1) + Fib(n-2)
Coin(amount) = min(Coin(amount - coin) + 1) for each coin
```

---

## Approaches

### 1. Top-Down (Memoization)
Recursive approach with caching.

#### Example: Fibonacci
```java
public class Fibonacci {
    static Map<Integer, Long> memo = new HashMap<>();
    
    public static long fib(int n) {
        // Base case
        if (n <= 1) return n;
        
        // Check memo
        if (memo.containsKey(n)) {
            return memo.get(n);
        }
        
        // Calculate and store
        long result = fib(n - 1) + fib(n - 2);
        memo.put(n, result);
        
        return result;
    }
    
    public static void main(String[] args) {
        System.out.println(fib(50));  // Fast: 12586269025
    }
}
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

### 2. Bottom-Up (Tabulation)
Iterative approach building from base cases.

#### Example: Fibonacci
```java
public class FibonacciDP {
    public static long fib(int n) {
        if (n <= 1) return n;
        
        // Create DP table
        long[] dp = new long[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        
        // Fill table
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
    
    public static void main(String[] args) {
        System.out.println(fib(50));  // 12586269025
    }
}
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

#### Space Optimized
```java
public static long fib(int n) {
    if (n <= 1) return n;
    
    long prev = 0, curr = 1;
    
    for (int i = 2; i <= n; i++) {
        long next = prev + curr;
        prev = curr;
        curr = next;
    }
    
    return curr;  // O(1) space
}
```

---

## Common Problems

### 1. Climbing Stairs
**Problem:** Climb n stairs, each time you can climb 1 or 2 steps. How many ways?

```java
public int climbStairs(int n) {
    if (n <= 2) return n;
    
    int[] dp = new int[n + 1];
    dp[1] = 1;  // 1 way to climb 1 stair
    dp[2] = 2;  // 2 ways to climb 2 stairs
    
    for (int i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    
    return dp[n];
}
// Time: O(n), Space: O(n)
```

### 2. Coin Change (Minimum Coins)
**Problem:** Minimum coins needed to make an amount.

```java
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);  // Initialize with max value
    dp[0] = 0;  // 0 coins needed for amount 0
    
    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (coin <= i) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    
    return dp[amount] > amount ? -1 : dp[amount];
}
// Time: O(amount * coins.length), Space: O(amount)
```

### 3. House Robber
**Problem:** Rob houses to maximize money. Can't rob adjacent houses.

```java
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[0];
    
    int[] dp = new int[nums.length];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);
    
    for (int i = 2; i < nums.length; i++) {
        dp[i] = Math.max(
            nums[i] + dp[i - 2],  // Rob current
            dp[i - 1]             // Skip current
        );
    }
    
    return dp[nums.length - 1];
}
// Time: O(n), Space: O(n)
```

### 4. 0/1 Knapsack
**Problem:** Pack items with max value within weight limit.

```java
public int knapsack(int[] weights, int[] values, int capacity) {
    int n = weights.length;
    int[][] dp = new int[n + 1][capacity + 1];
    
    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= capacity; w++) {
            if (weights[i - 1] <= w) {
                dp[i][w] = Math.max(
                    values[i - 1] + dp[i - 1][w - weights[i - 1]],
                    dp[i - 1][w]
                );
            } else {
                dp[i][w] = dp[i - 1][w];
            }
        }
    }
    
    return dp[n][capacity];
}
// Time: O(n * capacity), Space: O(n * capacity)
```

### 5. Longest Common Subsequence
**Problem:** Find LCS length of two strings.

```java
public int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length();
    int n = text2.length();
    int[][] dp = new int[m + 1][n + 1];
    
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }
    
    return dp[m][n];
}
// Time: O(m * n), Space: O(m * n)
```

---

## Steps to Solve DP Problem

1. **Define State** - What does dp[i] represent?
2. **Base Case** - What are the initial values?
3. **Recurrence Relation** - How to calculate dp[i]?
4. **Optimize** - Can we reduce space?

---

## Interview Questions

### Q1: What's the difference between memoization and tabulation?
**Answer:** Memoization is top-down (recursive) with caching. Tabulation is bottom-up (iterative) building from base cases.

### Q2: When is DP better than recursion?
**Answer:** When there are overlapping subproblems. DP avoids recalculating same subproblems.

### Q3: What's the time complexity of Fibonacci with and without DP?
**Answer:** Without DP: O(2^n). With DP: O(n).

### Q4: How to identify a DP problem?
**Answer:** Look for overlapping subproblems and optimal substructure. Can you break it into smaller subproblems?
