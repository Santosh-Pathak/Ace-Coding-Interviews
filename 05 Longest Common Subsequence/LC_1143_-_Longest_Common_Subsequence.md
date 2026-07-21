# o1 - LC 1143 - Longest Common Subsequence

Pattern: 05 Longest Common Subsequence

Problem: LC 1143 - Longest Common Subsequence
LeetCode / Source: LC 1143 - Longest Common Subsequence

Notes:

- Follow the pattern strategy for this topic.
- Use this file to store solutions, approach notes, and code snippets.

```cpp

class Solution {
public:
    int solveUsingRecursion(string text1, string text2,int i,int j)
    {
        if(i==text1.size())return 0;
        if(j==text2.size())return 0;

        if(text1[i] == text2[j])
            return 1 + solveUsingRecursion(text1,text2,i+1,j+1);
        else
            return 0 + max(solveUsingRecursion(text1,text2,i+1,j),solveUsingRecursion(text1,text2,i,j+1));

        return 0;
    }
    int longestCommonSubsequence(string text1, string text2) {
        int i=0,j=0;
        return solveUsingRecursion(text1,text2,i,j);
    }
};


class Solution {
public:
      int solveUsingMem(string &text1, string &text2,int i,int j,vector<vector<int>>&dp)
    {
        if(i==text1.size())return 0;
        if(j==text2.size())return 0;
        if(dp[i][j] != -1)return dp[i][j];
        int ans=0;
        if(text1[i] == text2[j])
            ans= 1 + solveUsingMem(text1,text2,i+1,j+1,dp);
        else
            ans= 0 + max(solveUsingMem(text1,text2,i+1,j,dp),solveUsingMem(text1,text2,i,j+1,dp));

        return dp[i][j] = ans;
    }
    int longestCommonSubsequence(string text1, string text2) {
        int i=0,j=0;
        // return solveUsingRecursion(text1,text2,i,j);

        vector<vector<int>>dp(text1.length(), vector<int>(text2.length(),-1));
        return solveUsingMem(text1,text2,i,j,dp);
    }
};
