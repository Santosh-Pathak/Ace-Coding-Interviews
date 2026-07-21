# o1 - LC 322 - Coin Change

Pattern: 03 Unbounded Knapsack

Problem: LC 322 - Coin Change
LeetCode / Source: LC 322 - Coin Change

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
class Solution {
public:
    const int INF = 1e9;

    int solve(vector<int>& coins, int amount, int i) {

        if (amount == 0)
            return 0;

        if (i >= coins.size())
            return INF;

        int skip = solve(coins, amount, i + 1);

        int take = INF;
        if (amount >= coins[i]) {
            take = 1 + solve(coins, amount - coins[i], i);
        }

        return min(take, skip);
    }

    int coinChange(vector<int>& coins, int amount) {

        int ans = solve(coins, amount, 0);

        return ans == INF ? -1 : ans;
    }
};

class Solution {
public:
    const int INF = 1e9;

    int solve(vector<int>& coins, int amount, int i,
              vector<vector<int>>& dp) {

        if (amount == 0)
            return 0;

        if (i >= coins.size())
            return INF;

        if (dp[i][amount] != -1)
            return dp[i][amount];

        // Take current coin
        int take = INF;
        if (amount >= coins[i]) {
            take = 1 + solve(coins, amount - coins[i], i, dp);
        }

        // Skip current coin
        int skip = solve(coins, amount, i + 1, dp);

        return dp[i][amount] = min(take, skip);
    }

    int coinChange(vector<int>& coins, int amount) {

        int n = coins.size();
        vector<vector<int>> dp(n, vector<int>(amount + 1, -1));

        int ans = solve(coins, amount, 0, dp);

        return ans == INF ? -1 : ans;
    }
};

```
