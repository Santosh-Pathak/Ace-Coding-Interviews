# o8 - LC 322 - Coin Change (1D variant)

Pattern: 01 Fibonacci Linear DP

Problem: LC 322 - Coin Change (1D variant)
LeetCode / Source: LC 322 - Coin Change (1D variant)

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int solve(vector<int>& coins, int T, int i) {

        if (i == 0) {
            if (T % coins[0] == 0)
                return T / coins[0];
            return 1e9;
        }

        int notPick = solve(coins, T, i - 1);

        int pick = 1e9;
        if (coins[i] <= T)
            pick = 1 + solve(coins, T - coins[i], i);

        return min(pick, notPick);
    }

    int coinChange(vector<int>& coins, int amount) {
        int ans = solve(coins, amount, coins.size() - 1);

        if (ans >= 1e9)
            return -1;

        return ans;
    }
};

class Solution {
public:
    int solve(vector<int>& coins, int T, int i, vector<vector<int>>& dp) {

        if (i == 0) {
            if (T % coins[0] == 0)
                return T / coins[0];
            return 1e9;
        }

        if (dp[i][T] != -1)
            return dp[i][T];

        int notPick = solve(coins, T, i - 1, dp);

        int pick = 1e9;
        if (coins[i] <= T)
            pick = 1 + solve(coins, T - coins[i], i, dp);

        return dp[i][T] = min(pick, notPick);
    }

    int coinChange(vector<int>& coins, int amount) {

        int n = coins.size();
        vector<vector<int>> dp(n, vector<int>(amount + 1, -1));

        int ans = solve(coins, amount, n - 1, dp);

        return (ans >= 1e9) ? -1 : ans;
    }
};
```
