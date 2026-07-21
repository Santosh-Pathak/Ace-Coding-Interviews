# o1 - LC 416 - Partition Equal Subset Sum

Pattern: 04 Subset Sum Partition

Problem: LC 416 - Partition Equal Subset Sum
LeetCode / Source: LC 416 - Partition Equal Subset Sum

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
class Solution {
public:
    bool solve(vector<int>& nums,int i,int t){

        if(t==0)return true;

        if(t<0)return false;
        if(i>=nums.size())return false;

        bool take = solve(nums,i+1,t-nums[i]);
        bool skip = solve(nums,i+1,t);

        return take||skip;
    }
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(begin(nums), end(nums),0);
        if (sum % 2 != 0)
            return false;

        return solve(nums,0,sum/2);
    }
};

class Solution {
public:
    bool solve(vector<int>& nums,int i,int t,vector<vector<int>>& dp){

        if(t==0)return true;

        if(t<0)return false;
        if(i>=nums.size())return false;

        if(dp[i][t]!=-1)return dp[i][t];
        bool take = solve(nums,i+1,t-nums[i],dp);
        bool skip = solve(nums,i+1,t,dp);

        dp[i][t] = take||skip;
        return dp[i][t];
    }
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(begin(nums), end(nums),0);
        if (sum % 2 != 0)
            return false;
            int n = nums.size();
            int t=sum/2;
        vector<vector<int>>dp(n,vector<int>(t+1,-1));
        return solve(nums,0,t,dp);
    }
};

```
