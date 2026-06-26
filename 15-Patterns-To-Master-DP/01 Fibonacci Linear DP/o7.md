# o7 - LC 1137 - N-th Tribonacci Number

Pattern: 01 Fibonacci Linear DP

Problem: LC 1137 - N-th Tribonacci Number
LeetCode / Source: LC 1137 - N-th Tribonacci Number

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
class Solution {
public:
    int solve(int n) {
        if (n == 0)
            return n;
        if (n == 1 || n == 2)
            return 1;

        return solve(n - 1) + solve(n - 2) + solve(n - 3);
    }
    int solveMemo(int n, vector<int>& dp) {
        if (n == 0)
            return 0;
        if (n == 1 || n == 2)
            return 1;
        if (dp[n] != -1)
            return dp[n];

        dp[n] =
            solveMemo(n - 1, dp) + solveMemo(n - 2, dp) + solveMemo(n - 3, dp);
        return dp[n];
    }
    int tribonacci(int n) {
        // approach 1, simnple recursive
        // return solve(n);

        // approach 2, recursion + dp(memoization)
        // vector<int>dp(n + 1, -1);
        // return solveMemo(n, dp);

        // approach 3, without using extra space
        int a = 0, b = 1, c = 1;
        if (n == 0)
            return 0;
        if (n == 1 || n == 2)
            return 1;
        int ans = 0;
        for (int i = 3; i <= n; i++) {
            ans = a + b + c;
            a = b;
            b = c;
            c = ans;
        }
        return ans;
    }
};

```
