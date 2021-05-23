
# Problem
### LeetCode 1143. Longest Common Subsequence
https://leetcode.com/problems/longest-common-subsequence

# Solution
```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {

        /**
         *  TC: O(M * N), where
         *      M is the length of the first string
         *      N is the length of the second string
         *
         *  SC: O(M * N)
         *
         *
         *  dp[i][j]: The LCS of the prefixes A(0, i) and B(0, j).
         *
         *  dp[i][j] = | if A[i] == B[j], dp[i - 1][j - 1] + 1
         *             | Otherwise      , MAX(dp[i - 1][j], dp[i][j - 1])
         */

        int n1 = text1.length();
        int n2 = text2.length();

        vector<vector<int>> dp(n1 + 1, vector<int>(n2 + 1, 0));

        for (int i = 1 ; i <= n1 ; ++i) {
            for (int j = 1 ; j <= n2 ; ++j) {
                if (text1[i - 1] == text2[j - 1]) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = std::max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }

        return dp[n1][n2];
    }
};
```

