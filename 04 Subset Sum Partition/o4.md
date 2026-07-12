# o4 - LC 2035 - Partition Array Into Two Arrays to Minimize Sum Difference

Pattern: 04 Subset Sum Partition

Problem: LC 2035 - Partition Array Into Two Arrays to Minimize Sum Difference
LeetCode / Source: LC 2035 - Partition Array Into Two Arrays to Minimize Sum Difference

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int totalSum;
    int ans;

    void solve(vector<int>& nums, int i, int curSum, int count, int n) {
        if (count == 0) {
            // curSum = sum of chosen n elements
            int other = totalSum - curSum;
            ans = min(ans, abs(curSum - other));
            return;
        }
        if (i >= nums.size()) return;

        solve(nums, i+1, curSum + nums[i], count-1, n);
        solve(nums, i+1, curSum, count, n);
    }

    int minimumDifference(vector<int>& nums) {
        totalSum = accumulate(begin(nums), end(nums), 0);
        int n = nums.size() / 2;
        ans = INT_MAX;

        solve(nums, 0, 0, n, n);

        return ans;
    }
};

```
