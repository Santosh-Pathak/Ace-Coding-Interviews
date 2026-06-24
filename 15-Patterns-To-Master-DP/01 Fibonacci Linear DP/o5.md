# o5 - LC 337 - House Robber III

Pattern: 01 Fibonacci Linear DP

Problem: LC 337 - House Robber III
LeetCode / Source: LC 337 - House Robber III

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

/**

- Definition for a binary tree node.
- struct TreeNode {
-     int val;
-     TreeNode *left;
-     TreeNode *right;
-     TreeNode() : val(0), left(nullptr), right(nullptr) {}
-     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
-     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
- };
 */

    // just like HR-2 problem, only we have to send a flag to children nodes to rob or not. ans whether to rob root or not.

```cpp

  class Solution {
public:
    int solve(TreeNode* root, bool canRob) {
        if (root == NULL) return 0;

        int rob =0;
        if(canRob){
         rob = root->val + solve(root->left, false) + solve(root->right, false);
        }
        int skip = solve(root->left, true) + solve(root->right, true);

        return max(rob, skip);
    }

    int rob(TreeNode* root) {
        return solve(root, true);
    }
};
```

```cpp

class Solution {
public:
    map<pair<TreeNode*, bool>, int> dp;

    int solve(TreeNode* root, bool canRob) {
        if (root == NULL) return 0;

        if (dp.count({root, canRob})) return dp[{root, canRob}];

        int rob = 0;
        if (canRob) {
            rob = root->val + solve(root->left, false) + solve(root->right, false);
        }
        int skip = solve(root->left, true) + solve(root->right, true);

        return dp[{root, canRob}] = max(rob, skip);
    }

    int rob(TreeNode* root) { return solve(root, true); }
};
```
