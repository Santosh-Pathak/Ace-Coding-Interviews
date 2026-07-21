# o3 - LC 1049 - Last Stone Weight II

Pattern: 02 0-1 Knapsack

Problem: LC 1049 - Last Stone Weight II
LeetCode / Source: LC 1049 - Last Stone Weight II

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp
/*
Say you have four stones a,b,c,d.
first you smash b against c, you get (b-c)
now you smash (b-c) against a
you get a-(b-c) which is same as (a+c)-(b)
now you smash d against (a+c)-b
you get d-((a+c)-b) which is same as (d+b)-(a+c).
Basically for the given stones we can create two sets,the sum of second set of stones to be subtracted from sum of first one.
ideally we want sum of each set to be sum(stones)/2 so that they cancel each other out.

So to solve the problem we try to select a set of stones such that their sum comes as close as possible to sum(stones)/2 from the lower side.
Clearly this subproblem is analogous to the knapsack problem.

Since we went from the lower side we have created the second set, that is the set to be subtracted. The first set then becomes sum-dp[n][sum/2].
Therefore the answer becomes sum-2*(dp[n][sum/2])

*/


class Solution {
public:
    int ans = 0;
    void solve(vector<int>& stones, int i, int t, int sum) {
        if (sum > t)
            return;

        if (i == stones.size()) {
            ans = max(ans, sum);
            return;
        }

        ans = max(ans, sum);
        solve(stones, i + 1, t, sum + stones[i]);
        solve(stones, i + 1, t, sum);
    }
    int lastStoneWeightII(vector<int>& stones) {
        int sum = accumulate(stones.begin(), stones.end(), 0);
        cout << sum << " ";
        int target = sum / 2;
        cout << target << " ";
        solve(stones, 0, target, 0);
        cout << ans << " ";
        int res = sum - (2 * ans);
        return res;
    }
};

class Solution {
public:
    int ans = 0;

    void solve(vector<int>& stones, int i, int target, int sum,
               vector<vector<int>>& dp) {

        if (sum > target)
            return;

        if (i == stones.size()) {
            ans = max(ans, sum);
            return;
        }

        if (dp[i][sum] != -1)
            return;

        dp[i][sum] = 1;

        // Take
        solve(stones, i + 1, target, sum + stones[i], dp);

        // Skip
        solve(stones, i + 1, target, sum, dp);
    }

    int lastStoneWeightII(vector<int>& stones) {
        int total = accumulate(stones.begin(), stones.end(), 0);
        int target = total / 2;

        vector<vector<int>> dp(stones.size(), vector<int>(target + 1, -1));

        solve(stones, 0, target, 0, dp);

        return total - 2 * ans;
    }
};

```
