# o9 - LC 983 - Minimum Cost For Tickets

Pattern: 01 Fibonacci Linear DP

Problem: LC 983 - Minimum Cost For Tickets
LeetCode / Source: LC 983 - Minimum Cost For Tickets

Notes:
- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int solve(vector<int>& days, vector<int>& cost, int index) {

        if (index >= days.size()) {
            return 0;
        }

        int j = index;

        // 1 day pass
        int one = cost[0] + solve(days, cost, index + 1);

        // 7 day pass
        while (j < days.size() && days[j] < days[index] + 7) {
            j++;
        }

        int seven = cost[1] + solve(days, cost, j);

        // 30 day pass
        int k = index;

        while (k < days.size() && days[k] < days[index] + 30) {
            k++;
        }

        int month = cost[2] + solve(days, cost, k);

        return min({one, seven, month});
    }

    int mincostTickets(vector<int>& days, vector<int>& costs) {
        return solve(days, costs, 0);
    }
};
```