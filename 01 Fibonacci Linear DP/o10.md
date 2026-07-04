# o10 - LC 91 - Decode Ways

Pattern: 01 Fibonacci Linear DP

Problem: LC 91 - Decode Ways
LeetCode / Source: LC 91 - Decode Ways

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
class Solution {
public:
    int solve(string& s, int index) {

        if (index == s.size()) {
            return 1;
        }

        if (s[index] == '0') {
            return 0;
        }

        int ways = 0;

        ways += solve(s, index + 1);

        if (index + 1 < s.size()) {

            int num = (s[index] - '0') * 10 + (s[index + 1] - '0');

            if (num >= 10 && num <= 26) {
                ways += solve(s, index + 2);
            }
        }

        return ways;
    }

    int numDecodings(string s) {
        return solve(s, 0); }
};

class Solution {
public:
    int solveMemo(string& s, int index, vector<int>& dp) {

        if (index == s.size()) {
            return 1;
        }

        if (s[index] == '0') {
            return 0;
        }
        if (dp[index] != -1)
            return dp[index];
        int ways = 0;

        ways += solveMemo(s, index + 1,dp);

        if (index + 1 < s.size()) {

            int num = (s[index] - '0') * 10 + (s[index + 1] - '0');

            if (num >= 10 && num <= 26) {
                ways += solveMemo(s, index + 2,dp);
            }
        }

        dp[index] = ways;
        return dp[index];
    }

    int numDecodings(string s) {
        vector<int> dp(s.size() + 1, -1);
        return solveMemo(s, 0, dp);
    }
};
```
