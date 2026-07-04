# o2 - LC 518 - Coin Change II

Pattern: 03 Unbounded Knapsack

Problem: LC 518 - Coin Change II
LeetCode / Source: LC 518 - Coin Change II

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int ans = 0;
    void solve(int amount, vector<int>& coins, int i) {

        if (amount < 0 || i >= coins.size()) {
            return;
        }

        if (amount == 0) {
            ans++;
            return;
        }

        if (amount >= coins[i]) {
            solve(amount - coins[i], coins, i);
        }
        solve(amount, coins, i + 1);
    }

    int solveMemo(int amount, vector<int>& coins, int i,
                  vector<vector<int>>& dp) {

        if (amount < 0 || i >= coins.size()) {
            return 0;
        }

        if (amount == 0) {
            return 1;
        }

        if (dp[i][amount] != -1)
            return dp[i][amount];

        int take = 0, skip = 0;

        if (amount >= coins[i]) {
            take = solveMemo(amount - coins[i], coins, i, dp);
        }
        
        skip = solveMemo(amount, coins, i + 1, dp);

        dp[i][amount] = take + skip;
        return dp[i][amount];
    }
    int change(int amount, vector<int>& coins) {

        // solve(amount, coins, 0);
        // return ans;
        int n = coins.size();
        vector<vector<int>> dp(n, vector<int>(amount + 1, -1));
        return solveMemo(amount, coins, 0, dp);
    }
};
```
