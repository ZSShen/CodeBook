
# Problem
### LeetCode 1035. Uncrossed Lines
https://leetcode.com/problems/uncrossed-lines/

# Solution
```c++
class Solution {
public:
    int maxUncrossedLines(vector<int>& S, vector<int>& T) {

        /**
         *  TC: O(S * T), where
         *      S is the length of string s
         *      T is the length of string t
         *
         *  SC: O(S * T)
         *
         *  dp[i][j]: The max number of uncrossing lines produced by using
         *            the first i numbers of A and the first j numbers of B.
         *
         *  dp[i][j] = | if S[i] == T[j], 1 + dp[i - 1][j - 1]
         *             | otherwise      , MAX | dp[i][j - 1]
         *                                    | dp[i + 1][j]
         */

        int ns = S.size();
        int nt = T.size();
        vector<vector<int>> dp(ns + 1, vector<int>(nt + 1));

        for (int i = 1 ; i <= ns ; ++i) {
            for (int j = 1 ; j <= nt ; ++j) {
                if (S[i - 1] == T[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[ns][nt];
    }
};
```