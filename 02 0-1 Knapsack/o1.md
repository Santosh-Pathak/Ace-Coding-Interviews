# o1 - LC 416 - Partition Equal Subset Sum

Pattern: 02 0-1 Knapsack

Problem: LC 416 - Partition Equal Subset Sum
LeetCode / Source: LC 416 - Partition Equal Subset Sum

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

class Solution {
public:
    bool solve(vector<int>& v, int target, int index) {
        int n = v.size();
        if (index >= n) {
            return false;
        }

        if (target < 0) {
            return false;
        }

        if (target == 0) {
            return true;
        }

        // Include the current element in the subset
        bool leftAns = solve(v, target - v[index], index + 1);

        // Exclude the current element from the subset
        bool rightAns = solve(v, target, index + 1);

        // Return true if either including or excluding the current element
        // leads to a solution
        return leftAns || rightAns;
    }

    bool solveUsingMemoisation(vector<int>& v, int target, int index,
                               vector<vector<int>>& dp) {
        int n = v.size();
        if (index >= n) {
            return false;
        }

        if (target < 0) {
            return false;
        }

        if (target == 0) {
            return true;
        }
        if (dp[index][target] != -1)
            return dp[index][target];

        // Include the current element in the subset
        bool leftAns =
            solveUsingMemoisation(v, target - v[index], index + 1, dp);

        // Exclude the current element from the subset
        bool rightAns = solveUsingMemoisation(v, target, index + 1, dp);

        // Return true if either including or excluding the current element
        // leads to a solution
        return dp[index][target] = (leftAns || rightAns);
    }

    bool canPartition(vector<int>& v) {
        int n = v.size();
        int sum = 0;
        for (auto x : v)
            sum += x;
        if (sum & 1)
            return false; // if sum is Odd therefore return false beacuse sum
                          // can;t be halfed
        int target = sum / 2;
        int index = 0;
        //  return solve(v,target,index);

        vector<vector<int>> dp(n + 1, vector<int>(target + 1, -1));
        return solveUsingMemoisation(v, target, index, dp);
    }
};
