# o4 - LC 213 - House Robber II

Pattern: 01 Fibonacci Linear DP

Problem: LC 213 - House Robber II
LeetCode / Source: LC 213 - House Robber II

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

## Approach and Explanation

- **Problem summary:** Houses are arranged in a circle; adjacent houses cannot both be robbed. This is like House Robber I (linear) but with a circular constraint between the first and last houses.
- **Key idea:** Break the circle into two linear cases and solve each with the standard linear House Robber algorithm:
  - Case A: Rob houses in range [0, n-2] (exclude last house)
  - Case B: Rob houses in range [1, n-1] (exclude first house)
  - Answer = max(caseA, caseB)
- **Why this works:** In any valid solution either house 0 is not robbed or house n-1 is not robbed (because they are adjacent). The two cases enumerate those possibilities without overlap.
- **Complexity:** Each linear pass is O(n) time and O(n) space (can be reduced to O(1) by tracking two variables). Overall O(n) time, O(n) space.

### Solutions in this file

- The first code block is a simple recursive (exponential) solution for clarity — useful for understanding, but not efficient for large n.
- The second code block is a memoized (top-down DP) version which caches subproblems to make it O(n).
- The third code block is a bottom-up tabulation version (linear DP) which is the most idiomatic and easy to optimize to O(1) space.

### Annotated code (notes inline)

```cpp
// Recursive (exponential) — educational only
class Solution {
public:
    // Solve the linear robber on range [i, n-1) where n is exclusive bound.
    int solve(int i, vector<int>& nums, int n){
        // base: reached or passed the end
        if(i>=n) return 0;

        // choose to rob current house i, then skip i+1
        int collect = nums[i] + solve(i+2, nums, n);
        // or skip current house
        int skip = solve(i+1, nums, n);

        // return the better of robbing or skipping
        return max(collect, skip);
    }

    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n==1) return nums[0];
        if(n==2) return max(nums[0], nums[1]);
        // run two linear cases to handle circular adjacency
        return max(solve(0, nums, n-1),  // consider houses [0..n-2]
                   solve(1, nums, n));   // consider houses [1..n-1]
    }
};
```

```cpp
// Memoized top-down DP (O(n) time)
class Solution {
public:
    // solve on interval [i, end) with memoization in dp
    int solve(vector<int>& nums, int i, int end, vector<int>& dp) {
        if (i >= end) return 0;          // no houses left
        if (dp[i] != -1) return dp[i];   // cached result

        int collect = nums[i] + solve(nums, i + 2, end, dp); // rob i
        int skip = solve(nums, i + 1, end, dp);              // skip i

        return dp[i] = max(collect, skip);
    }

    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return nums[0];
        if (n == 2) return max(nums[0], nums[1]);

        // dp vectors sized n; when solving [0..n-2] we will only fill indices < n-1
        vector<int> dp1(n, -1), dp2(n, -1);
        // solve two cases and take max
        return max(solve(nums, 0, n - 1, dp1), // exclude last
                   solve(nums, 1, n, dp2));    // exclude first
    }
};
```

```cpp
// Bottom-up tabulation (O(n) time, O(n) space — can be reduced to O(1))
class Solution {
public:
    // solve linear interval [start, end) using DP table
    int solve(vector<int>& nums, int start, int end) {
        int n = end - start;               // number of houses in this interval
        if (n == 1)
            return nums[start];

        vector<int> dp(n);
        // dp[i] represents best robber value for subarray of length i+1
        dp[0] = nums[start];
        dp[1] = max(nums[start], nums[start + 1]);

        for (int i = 2; i < n; i++) {
            // either skip current (dp[i-1]) or rob current (nums[start+i] + dp[i-2])
            dp[i] = max(dp[i - 1], nums[start + i] + dp[i - 2]);
        }

        return dp[n - 1];
    }

    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 1)
            return nums[0];
        if (n == 2)
            return max(nums[0], nums[1]);

        // Solve two linear ranges to handle circular adjacency
        return max(solve(nums, 0, n - 1), // houses [0..n-2]
                   solve(nums, 1, n));    // houses [1..n-1]
    }
};

// Note: To reduce space to O(1), replace the dp vector with two variables "prev" and "curr"
// that maintain dp[i-2] and dp[i-1] respectively while iterating.
```
