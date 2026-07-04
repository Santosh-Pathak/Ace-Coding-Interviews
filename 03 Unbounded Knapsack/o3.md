# o3 - LC 279 - Perfect Squares

Pattern: 03 Unbounded Knapsack

Problem: LC 279 - Perfect Squares
LeetCode / Source: LC 279 - Perfect Squares

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    const int INF = 1e9;

    int solve(int i, int x, int n) {

        if (n == 0)
            return 0;

        if (i > x)
            return INF;

        int take = INF, skip = INF;

        if (i * i <= n) {
            take = 1 + solve(i, x, n - i * i);
        }

        skip = solve(i + 1, x, n);

        return min(take, skip);
    }

    int numSquares(int n) {

        int x = sqrt(n);

        return solve(1, x, n);
    }
};

