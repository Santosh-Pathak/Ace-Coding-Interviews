# o3 - LC 1723 - Find Minimum Time to Finish All Jobs

Pattern: 04 Subset Sum Partition

Problem: LC 1723 - Find Minimum Time to Finish All Jobs
LeetCode / Source: LC 1723 - Find Minimum Time to Finish All Jobs

Notes:
- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.


```cpp

class Solution {
public:
    bool solve(vector<int>& nums, vector<bool>& visited, int k, int target, int curSum, int idx) {
        if (k == 0) return true;
        if (curSum == target)
            return solve(nums, visited, k-1, target, 0, 0); // start fresh for next subset

        for (int i = idx; i < nums.size(); i++) {
            if (visited[i]) continue;
            if (curSum + nums[i] > target) continue;

            visited[i] = true;
            if (solve(nums, visited, k, target, curSum + nums[i], i+1))
                return true;
            visited[i] = false; // backtrack
        }

        return false;
    }

    bool canPartitionKSubsets(vector<int>& nums, int k) {
        int total = 0;
        for (int x : nums) total += x;

        if (total % k != 0) return false;FF

        int target = total / k;

        for (int x : nums)
            if (x > target) return false;

        vector<bool> visited(nums.size(), false);
        return solve(nums, visited, k, target, 0, 0);
    }
};

```