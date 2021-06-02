
# Problem
### LintCode 581. Longest Repeating Subsequence
https://www.lintcode.com/problem/longest-repeating-subsequence/description

# Solution
```c++
class Solution {
public:
    int longestPalindromeSubseq(string s) {

        /**
         *  TC: O(S^2), where
         *      S is the length of string s
         *
         *  SC: O(S^2)
         *
         *  dp[i][j]: The length of the longest common subsequence that can
         *            be found in the prefix of str ending at the index i and
         *            the prefix of str ending at the index j.
         *
         *  dp[i][j] = | if s[i] == s[j], | if i != j, dp[i - 1][j - 1] + 1
         *             |                  | otherwise, 0
         *             |
         *             | otherwise      , MAX{ dp[i][j - 1], dp[i - 1][j] }
         */

        int n = s.length();

        vector<vector<int>> dp(n, vector<int>(n));

        for (int i = 0 ; i < n ; ++i) {
            dp[i][i] = 1;
            if (i < n - 1) {
                dp[i][i + 1] = 1 + (s[i] == s[i + 1]);
            }
        }

        for (int l = 3 ; l <= n ; ++l) {
            for (int i = 0, j = i + l - 1 ; i <= n - l ; ++i, ++j) {
                if (s[i] == s[j]) {
                    dp[i][j] = 2 + dp[i + 1][j - 1];
                } else {
                    dp[i][j] = max(dp[i][j - 1], dp[i + 1][j]);
                }
            }
        }

        return dp[0][n - 1];
    }
};
```