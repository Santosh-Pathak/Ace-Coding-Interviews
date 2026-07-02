# 01 Fibonacci Linear DP

This README gives a per-question quick tutor explanation: the DP pattern used, why it fits, a short recurrence/template, base cases, complexity, and a brief tip. At the end is a folder summary listing the most used / important DP patterns for quick revision.

Problems (per-file notes)

Climbing Stairs (LC 70) — file: o1.md
- Pattern: Fibonacci / Linear DP (counting ways).
- Why: Number of ways to reach step i depends on a fixed small set of previous steps (i-1, i-2).
- Recurrence: ways[i] = ways[i-1] + ways[i-2]
- Base cases: ways[0]=1, ways[1]=1
- Complexity: O(n) time, O(1) space with rolling variables.
- Tip: Use two variables instead of an array for O(1) space.

Min Cost Climbing Stairs (LC 746) — file: o2.md
- Pattern: Linear DP (min-cost with bounded lookback).
- Why: Cost to reach i is cost[i] + min(cost to reach previous allowed steps).
- Recurrence: dp[i] = cost[i] + min(dp[i-1], dp[i-2])
- Base cases: dp[0]=cost[0], dp[1]=cost[1]
- Complexity: O(n) time, O(1) space.

House Robber (LC 198) — file: o3.md
- Pattern: Linear DP (max-collect without adjacent picks).
- Why: At house i you choose max of robbing it + dp[i-2] or skipping it dp[i-1].
- Recurrence: dp[i] = max(dp[i-1], nums[i] + dp[i-2])
- Base cases: dp[0]=nums[0], dp[1]=max(nums[0], nums[1])
- Tip: Rolling two variables suffice.

House Robber II (LC 213) — file: o4.md
- Pattern: Linear DP on circular array (apply linear twice).
- Why: Circle breaks linear recurrence at endpoints — split into two linear problems excluding one endpoint each time.
- Approach: Solve two linear DP runs: [0..n-2] and [1..n-1], take max.

House Robber III (LC 337) — file: o5.md
- Pattern: Tree DP (post-order linear-like choices per node).
- Why: Tree nodes choose whether to rob current node and skip children or not.
- Recurrence: For node: rob = val + sum(notRob(child)); notRob = sum(max(rob(child), notRob(child))).
- Approach: DFS post-order, return pair (rob, notRob).

Fibonacci Number (LC 509) — file: o6.md
- Pattern: Fibonacci / Linear DP (classic recurrence).
- Recurrence: fib[n] = fib[n-1] + fib[n-2] with fib[0]=0, fib[1]=1.
- Complexity: O(n), O(1) space with rolling variables or O(log n) using matrix exponentiation.

N-th Tribonacci Number (LC 1137) — file: o7.md
- Pattern: Linear DP with larger fixed window (k-step recurrence).
- Recurrence: t[n] = t[n-1] + t[n-2] + t[n-3]
- Tip: Generalize rolling window to k previous states.

Coin Change (LC 322) — file: o8.md
- Pattern: Linear / Unbounded-variation (min coins to form amount).
- Why: For each amount, look at previous amounts reachable by subtracting coin value.
- Recurrence: dp[a] = min(dp[a], 1 + dp[a-coin]) for each coin
- Base: dp[0]=0, dp[>0]=inf initially.
- Complexity: O(amount * #coins)

Minimum Cost For Tickets (LC 983) — file: o9.md
- Pattern: Linear DP with intervals (lookahead choices of passes of length 1/7/30).
- Recurrence: dp[i] = min(cost1 + dp[i+1], cost7 + dp[nextDayAfter7], cost30 + dp[nextDayAfter30]) when iterating days backward or forward with memo.
- Tip: Iterate days in increasing order using mapping from day->index or use recursion+memo.

Decode Ways (LC 91) — file: o10.md
- Pattern: Linear DP with constrained transitions (counting valid partitions).
- Recurrence: dp[i] = (valid1(i) ? dp[i-1] : 0) + (valid2(i-1,i) ? dp[i-2] : 0)
- Base: dp[0]=1, dp[1]=1 or 0 depending on first char.

---

Folder summary — most used / important DP ideas in this folder
- Core pattern: Fibonacci / Linear DP (fixed small window dependencies). Most problems reduce to defining dp[i] as best/count/cost up to i and combining a fixed number of prior states.
- Common optimizations: space-optimization to O(1) using rolling variables; generalize to k-step recurrences; reduction of circular cases to two linear runs.
- Secondary pattern: Tree DP (post-order) appears for tree-structured variants like `o5`.

If you'd like, I can: convert each per-question note into a one-page printable flashcard, or apply the same per-question README format to other pattern folders.

---

This folder focuses on: Fibonacci / Linear DP

Key idea
- Problems where dp[i] depends on a small fixed set of previous states (i-1, i-2, etc.).

Standard approach (Tutor steps)
1. Identify the state: what does dp[i] represent? (e.g., number of ways, minimum cost, max profit)
2. Write recurrence using previous indices: dp[i] = combine(dp[i-1], dp[i-2], ...).
3. Set base cases for smallest i (often dp[0], dp[1]).
4. Choose iteration order (usually increasing i for linear DP).
5. If possible, optimize space (keep only last k states).
6. Validate on sample cases and edge cases (empty, single element, large N).

Template (iterative, 1D)

```python
# Example: linear DP skeleton
def solve(n):
	dp = [0]*(n+1)
	dp[0] = base0
	dp[1] = base1
	for i in range(2, n+1):
		dp[i] = f(dp[i-1], dp[i-2])
	return dp[n]
```

Space optimization tip: if recurrence uses only k previous values, keep a fixed-size deque or variables and update rolling values.

Common pitfalls
- Missing or wrong base cases.
- Wrong iteration direction when recurrence references future states.
- Off-by-one on indices (0-based vs 1-based).


Quick revision checklist

- Read the problem and name the state in one sentence.
- Write the recurrence on a whiteboard or notebook before coding.
- Identify base cases and small n behavior.
- Decide whether 1D rolling array suffices.
- Dry-run on small inputs and edge cases.

If you want, I can similarly add a one-page cheat-sheet PDF or printable cards for quick offline revision.

