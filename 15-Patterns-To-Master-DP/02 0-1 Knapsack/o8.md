# o8 - LC 2915 - Length of the Longest Subsequence That Sums to Target

Pattern: 02 0-1 Knapsack

Problem: LC 2915 - Length of the Longest Subsequence That Sums to Target
LeetCode / Source: LC 2915 - Length of the Longest Subsequence That Sums to Target

Notes:
- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int solve(vector<int>& nums, int target, int i) {

        if (target == 0)
            return 0;

        if (i == nums.size() || target < 0)
            return -1e9;

        int take = 1 + solve(nums, target - nums[i], i + 1);
        int skip = solve(nums, target, i + 1);

        return max(take, skip);
    }

    int lengthOfLongestSubsequence(vector<int>& nums, int target) {

        int ans = solve(nums, target, 0);

        return (ans < 0) ? -1 : ans;
    }
};

