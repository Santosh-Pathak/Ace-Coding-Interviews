# o2 - LC 494 - Target Sum

Pattern: 02 0-1 Knapsack

Problem: LC 494 - Target Sum
LeetCode / Source: LC 494 - Target Sum

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int rec(vector<int>& nums, int target, int i) {
        if (i == nums.size()) return target == 0 ? 1 : 0;

        int inc = rec(nums, target - nums[i], i + 1);
        int exc = rec(nums, target + nums[i], i + 1);

        return inc + exc;
    }

    int findTargetSumWays(vector<int>& nums, int target) {
         return rec(nums, target, 0);
    }
};

```
