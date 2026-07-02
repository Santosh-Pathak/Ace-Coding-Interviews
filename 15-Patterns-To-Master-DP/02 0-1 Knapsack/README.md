# 02 0-1 Knapsack

This README lists each problem in the folder with the DP pattern used, brief reasoning, recurrence or template, base cases, complexity, and a final folder summary highlighting the most used / important patterns for quick revision.

Problems (per-file notes)

Partition Equal Subset Sum (LC 416) — file: o1.md
- Pattern: Subset Sum (0-1 knapsack reduction to boolean feasibility).
- Why: Can we select a subset summing to total/2 — classic subset-sum DP.
- Recurrence (boolean): dp[i][s] = dp[i-1][s] or dp[i-1][s-nums[i]]
- 1D optimized: for s from target down to nums[i]: dp[s] |= dp[s-nums[i]]
- Complexity: O(n*sum), space O(sum) with 1D bitset/boolean.

Target Sum (LC 494) — file: o2.md
- Pattern: Subset Sum / Transform to 0-1 knapsack (partition with sign mapping).
- Why: Count ways to assign +/- to reach target -> reduce to subset sum of (sum+target)/2.
- Approach: transform and run subset-sum count DP.

Last Stone Weight II (LC 1049) — file: o3.md
- Pattern: Subset Sum (partition to minimize difference) — 0-1 knapsack variant.
- Why: Partition stones into two groups to minimize difference; equivalent to finding reachable sums close to total/2.

Ones and Zeroes (LC 474) — file: o4.md
- Pattern: 0-1 Knapsack with two-dimensional capacity (zeros and ones counts).
- Recurrence: dp[i][z][o] = max(dp[i-1][z][o], 1 + dp[i-1][z-zeros_i][o-ones_i])
- 1D optimization: iterate z and o descending to avoid reuse.

Profitable Schemes (LC 879) — file: o5.md
- Pattern: 0-1 Knapsack with two constraints (profit threshold and group size) — count ways DP with caps.

Toss Strange Coins (LC 1230) — file: o6.md
- Pattern: Probability DP — linear convolution-like DP across coin flips (counts or probabilities across successes).

Flowers (CF 474D) — file: o7.md
- Pattern: 0-1 Knapsack variant on combinatorial counts.

Length of the Longest Subsequence That Sums to Target (LC 2915) — file: o8.md
- Pattern: DP on subsequences with sum constraint — uses knapsack-like state tracking best length per sum.

Tallest Billboard (LC 956) — file: o9.md
- Pattern: Balanced-partition DP (difference-of-sums technique) — often solved by mapping states to difference -> dp[diff] = max height achievable.

Find the Maximum Length of a Good Subsequence II (LC 3177) — file: o10.md
- Pattern: DP with constraints on subsequence structure; often reducible to knapsack-like state transitions.

---

Folder summary — most used / important DP ideas in this folder
- Core patterns: 0-1 Knapsack and Subset Sum reductions. Many problems are either direct knapsack or can be transformed into subset-sum / partition instances.
- Important techniques: 1D capacity optimization (iterate capacity descending), transform-based reductions (map problem to subset-sum), using difference states (for balanced partitions), and multi-dimensional capacity DP for combinatorial constraints.
- Performance tips: use bitsets for large-sum boolean subset-sum, and iterate capacities descending to prevent reusing items.

If you'd like, I can apply the same per-question README format to the remaining pattern folders automatically.

---

This folder focuses on: 0-1 Knapsack

Key idea
- For each item, you either take it once or skip it. The DP state typically captures items considered and capacity/constraint.

Standard approach (Tutor steps)
1. Identify the state: dp[i][w] = best value using first i items with capacity w (or boolean feasibility).
2. Recurrence: dp[i][w] = max(dp[i-1][w], value[i] + dp[i-1][w-weight[i]]) when weight[i] <= w.
3. Base cases: dp[0][*] = 0 or false appropriately.
4. Iteration order: for i in items: for w from maxW down to weight[i] (for 1D optimization) OR w from 0..maxW for 2D.
5. Space optimization: use 1D dp[w] and iterate w descending to avoid reuse of same item.

Template (2D)

```python
dp = [[0]*(W+1) for _ in range(n+1)]
for i in range(1, n+1):
	for w in range(0, W+1):
		dp[i][w] = dp[i-1][w]
		if w >= wt[i]:
			dp[i][w] = max(dp[i][w], val[i] + dp[i-1][w-wt[i]])
```

Template (1D optimized)

```python
dp = [0]*(W+1)
for i in range(1, n+1):
	for w in range(W, wt[i]-1, -1):
		dp[w] = max(dp[w], val[i] + dp[w-wt[i]])
```

Common pitfalls
- Using ascending weight order with 1D array (causes reuse of same item multiple times).
- Off-by-one indexing when mapping items to dp indices.
- Confusing 0-1 and unbounded knapsack templates — iteration direction and loops differ.

Quick revision checklist

- Write the knapsack recurrence and identify whether problem is 0-1 or unbounded.
- Decide if the problem is value- or weight-constrained (some variants invert roles).
- For 1D optimization always iterate capacity descending.
- Test small n and boundary capacities (0, capacity exactly equal to weight of one item).

Want a printable two-column flashcard summary for offline review? I can generate it.

