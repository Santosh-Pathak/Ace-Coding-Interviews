# o4 - LC 474 - Ones and Zeroes

Pattern: 02 0-1 Knapsack

Problem: LC 474 - Ones and Zeroes
LeetCode / Source: LC 474 - Ones and Zeroes

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
class Solution {
public:
    pair<int, int> countChar(string str) {
        int zero = 0;
        int one = 0;
        for (auto x : str) {
            if (x == '0')
                zero++;
            else
                one++;
        }
        return {zero, one};
    }
    int solve(vector<string>& strs, int i, int m, int n) {

        if (i >= strs.size())
            return 0;

        if (m < 0 || n < 0)
            return INT_MIN;
        auto [xcount, ycount] = countChar(strs[i]);
        int pickCurrentStr = 0;
        if (xcount <= m && ycount <= n) {
            pickCurrentStr = 1 + solve(strs, i + 1, m - xcount, n - ycount);
        }
        int notPick = solve(strs, i + 1, m, n);

        return max(pickCurrentStr, notPick);
    }

    int solveMemo(vector<string>& strs, int i, int m, int n,
                  vector<vector<vector<int>>>& dp) {

        if (i >= strs.size())
            return 0;

        if (m < 0 || n < 0)
            return INT_MIN;

        if (dp[i][m][n] != -1)
            return dp[i][m][n];
        auto [xcount, ycount] = countChar(strs[i]);
        int pickCurrentStr = 0;
        if (xcount <= m && ycount <= n) {
            pickCurrentStr =
                1 + solveMemo(strs, i + 1, m - xcount, n - ycount, dp);
        }
        int notPick = solveMemo(strs, i + 1, m, n, dp);

        dp[i][m][n] = max(pickCurrentStr, notPick);
        return dp[i][m][n];
    }

    int findMaxForm(vector<string>& strs, int m, int n) {
        // return solve(strs, 0, m, n);
        vector<vector<vector<int>>> dp(
            strs.size(), vector<vector<int>>(m + 1, vector<int>(n + 1, -1)));
        return solveMemo(strs, 0, m, n, dp);
    }
};


class Solution {
public:
    pair<int, int> countChar(string str) {
        int zero = 0;
        int one = 0;

        for (char ch : str) {
            if (ch == '0')
                zero++;
            else
                one++;
        }

        return {zero, one};
    }

    int findMaxForm(vector<string>& strs, int m, int n) {

        int sz = strs.size();

        vector<vector<vector<int>>> dp(
            sz + 1,
            vector<vector<int>>(m + 1, vector<int>(n + 1, 0))
        );

        for (int i = sz - 1; i >= 0; i--) {

            auto [zeroCnt, oneCnt] = countChar(strs[i]);

            for (int j = 0; j <= m; j++) {

                for (int k = 0; k <= n; k++) {

                    int pick = 0;

                    if (zeroCnt <= j && oneCnt <= k) {
                        pick = 1 + dp[i + 1][j - zeroCnt][k - oneCnt];
                    }

                    int notPick = dp[i + 1][j][k];

                    dp[i][j][k] = max(pick, notPick);
                }
            }
        }

        return dp[0][m][n];
    }
};



```
