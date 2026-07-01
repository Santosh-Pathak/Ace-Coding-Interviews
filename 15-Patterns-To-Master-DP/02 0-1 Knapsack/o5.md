# o5 - LC 879 - Profitable Schemes

Pattern: 02 0-1 Knapsack

Problem: LC 879 - Profitable Schemes
LeetCode / Source: LC 879 - Profitable Schemes

Notes:
- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp



class Solution {
public:
    int MOD = 1e9 + 7;

    int solve(int n, int minProfit, vector<int>& group, vector<int>& profit,
              int i) {

        if (i == group.size()) {
            return (minProfit == 0);
        }

        int skipCurrentProfit = solve(n, minProfit, group, profit, i + 1);

        int takeCurrentProfit = 0;
        if (group[i] <= n) {
            takeCurrentProfit =
                solve(n - group[i], max(0, minProfit - profit[i]), group,
                      profit, i + 1);
        }

        return (takeCurrentProfit + skipCurrentProfit) % MOD;
    }

    int profitableSchemes(int n, int minProfit, vector<int>& group,
                          vector<int>& profit) {

        return solve(n, minProfit, group, profit, 0);
    }
};

class Solution {
public:
    const int MOD = 1e9 + 7;
    vector<vector<vector<int>>> dp;

    int solve(int n, int minProfit, vector<int>& group, vector<int>& profit,
              int i) {

        if (i == group.size())
            return (minProfit == 0);

        if (dp[i][n][minProfit] != -1)
            return dp[i][n][minProfit];

        int takeCurrentProfit = 0;
        if (group[i] <= n) {
            takeCurrentProfit =
                solve(n - group[i], max(0, minProfit - profit[i]), group,
                      profit, i + 1);
        }

        int skipCurrentProfit = solve(n, minProfit, group, profit, i + 1);

        return dp[i][n][minProfit] =
                   (takeCurrentProfit + skipCurrentProfit) % MOD;
    }

    int profitableSchemes(int n, int minProfit, vector<int>& group,
                          vector<int>& profit) {

        int m = group.size();

        dp.assign(m + 1,
                  vector<vector<int>>(n + 1, vector<int>(minProfit + 1, -1)));

        return solve(n, minProfit, group, profit, 0);
    }
};


```