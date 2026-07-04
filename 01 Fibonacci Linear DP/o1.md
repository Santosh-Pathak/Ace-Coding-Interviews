# o1 - LC 70 - Climbing Stairs

Pattern: 01 Fibonacci Linear DP

Problem: LC 70 - Climbing Stairs
LeetCode / Source: LC 70 - Climbing Stairs

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

// APPROACH 1: Naive Recursion
// Time: O(2^n), Space: O(n) recursion stack
// TLE on large inputs

```cpp
class Solution {
public:
    int solve(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        return solve(n-1) + solve(n-2);
    }

    int climbStairs(int n) {
        return solve(n);
    }
};
```

// APPROACH 2: Memoization (Top-Down DP)
// Time: O(n), Space: O(n) - memo array + recursion stack

```cpp
class Solution {
public:
    int solve(int n, vector<int>& memo) {
        if (n == 0 || n == 1) {
            return 1;
        }
        if (memo[n] != -1) {
            return memo[n];
        }
        memo[n] = solve(n-1, memo) + solve(n-2, memo);
        return memo[n];
    }

    int climbStairs(int n) {
        vector<int> memo(n+1, -1);
        return solve(n, memo);
    }
};
```

// APPROACH 3: Tabulation (Bottom-Up DP) - OPTIMAL
// Time: O(n), Space: O(n)
// REVISION NOTES:
// - Base cases: dp[0]=1 (one way), dp[1]=1 (one way)
// - Recurrence: dp[i] = dp[i-1] + dp[i-2]
// - Key insight: Fibonacci-like pattern

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }

        vector<int> dp(n + 1);
        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }

        return dp[n];
    }
};
```
