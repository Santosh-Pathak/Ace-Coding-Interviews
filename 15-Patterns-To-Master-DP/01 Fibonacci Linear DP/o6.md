# o6 - LC 509 - Fibonacci Number

Pattern: 01 Fibonacci Linear DP

Problem: LC 509 - Fibonacci Number
LeetCode / Source: LC 509 - Fibonacci Number

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

// For the Fibonacci problem, we use a linear DP pattern with space optimization.

```cpp
class Solution {
public:
    int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;

        int prev2 = 0; // fib(0)
        int prev1 = 1; // fib(1)
        int curr = 0;

        for (int i = 2; i <= n; i++) {
            curr = prev1 + prev2;
            prev2 = prev1;
            prev1 = curr;
        }

        return curr;
    }
};
```

```cpp

class Solution {
public:
    int fib(int n) {
   
        if(n==0 || n==1)return n;

        int a = 0;
        int b = 1;
        int c=0;
        for(int i=2;i<=n;i++)
        {   
            c=a+b;
            a=b;
            b=c;
        }
        
        return c;
    }
};

```

```cpp

class Solution {
public:
    int fib(int n) {
        int ans;
        if(n==0)
            return 0;
        if(n==1)
            return 1;
        
         ans = fib(n-1)+fib(n-2);
        
        return ans;
    }
};
```
