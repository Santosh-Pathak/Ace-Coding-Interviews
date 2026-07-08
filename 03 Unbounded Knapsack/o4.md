# o4 - LC 377 - Combination Sum IV

Pattern: 03 Unbounded Knapsack

Problem: LC 377 - Combination Sum IV
LeetCode / Source: LC 377 - Combination Sum IV

Notes:
- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
class Solution {
public:
    int solve(vector<int>& nums, int target) {
        if (target == 0) return 1;
        if (target < 0) return 0;

        int ans = 0;

        for (int i = 0; i < nums.size(); i++) {
            ans += solve(nums, target - nums[i]);
        }

        return ans;
    }

    int combinationSum4(vector<int>& nums, int target) {
        return solve(nums, target);
    }
};


class Solution {
public:
    vector<int> dp;

    int solve(vector<int>& nums, int target) {
        if (target == 0) return 1;
        if (target < 0) return 0;

        if (dp[target] != -1)
            return dp[target];

        long long ans = 0;

        for (int i = 0; i < nums.size(); i++) {
            ans += solve(nums, target - nums[i]);
        }

        return dp[target] = ans;
    }

    int combinationSum4(vector<int>& nums, int target) {
        dp.assign(target + 1, -1);
        return solve(nums, target);
    }
};
```