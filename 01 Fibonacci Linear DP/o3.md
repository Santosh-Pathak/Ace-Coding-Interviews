# o3 - LC 198 - House Robber

Pattern: 01 Fibonacci Linear DP

Problem: LC 198 - House Robber
LeetCode / Source: LC 198 - House Robber

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

// APPROACH 1: Naive Recursion
// - Try robbing each house or skipping it
// - Use recursion to explore both choices
// - Exponential time: O(2^n)
// - Only useful to understand the problem structure

```cpp
class Solution {
public:
    int collectMoney(int i, vector<int>& nums) {
        if (i >= nums.size()) {
            return 0; // no more houses to rob
        }

        int robCurrent = nums[i] + collectMoney(i + 2, nums);
        int skipCurrent = collectMoney(i + 1, nums);
        return max(robCurrent, skipCurrent);
    }

    int rob(vector<int>& nums) {
        if (nums.empty()) {
            return 0;
        }
        return collectMoney(0, nums);
    }
};
```

// APPROACH 2: Memoization (Top-Down DP)
// - Save results for subproblems to avoid repeated work
// - Time: O(n), Space: O(n)

```cpp
class Solution {
public:
    int collectMoney(int i, vector<int>& nums, vector<int>& dp) {
        if (i >= nums.size()) {
            return 0;
        }
        if (dp[i] != -1) {
            return dp[i]; // reuse cached answer
        }

        int robCurrent = nums[i] + collectMoney(i + 2, nums, dp);
        int skipCurrent = collectMoney(i + 1, nums, dp);
        dp[i] = max(robCurrent, skipCurrent);
        return dp[i];
    }

    int rob(vector<int>& nums) {
        if (nums.empty()) {
            return 0;
        }

        int n = nums.size();
        vector<int> dp(n, -1);
        return collectMoney(0, nums, dp);
    }
};
```

// APPROACH 3: Tabulation (Bottom-Up DP)
// - Build up the answer from the smallest subproblems
// - dp[i] = maximum money robbable from first i+1 houses
// - Time: O(n), Space: O(n)

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return nums[0];
        }

        vector<int> dp(n);

        // Base cases
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);

        // Fill dp array using the recurrence
        for (int i = 2; i < n; i++) {
            dp[i] = max(dp[i - 1], nums[i] + dp[i - 2]);
        }

        return dp[n - 1];
    }
};
```
