
# Problem
### LeetCode 97. Interleaving String
https://leetcode.com/problems/interleaving-string

# Solution
```c++
class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {

        /**
         *  TC: O(S1 * S2), where
         *      S1 is the length of string s1
         *      S2 is the length of string s2
         *
         *  SC: O(S1 * S2)
         *
         *
         *  dp[i][j]: Whether we can form the first (i + j) characters of S3
         *            by using the first i characters of S1 and the first j
         *            characters of S2.
         *
         *  dp[i][j] = (S1[i] == S3[i + j] && dp[i - 1][j]) ||
         *             (S2[j] == S3[i + j] && dp[i][j - 1])
         */

        int n1 = s1.length();
        int n2 = s2.length();
        int n3 = s3.length();

        if (n1 + n2 != n3) {
            return false;
        }

        vector<vector<bool>> dp(n1 + 1, vector<bool>(n2 + 1));
        dp[0][0] = true;

        for (int i = 1 ; i <= n1 ; ++i) {
            if (s3[i - 1] == s1[i - 1] && dp[i - 1][0]) {
                dp[i][0] = true;
            }
        }
        for (int i = 1 ; i <= n2 ; ++i) {
            if (s3[i - 1] == s2[i - 1] && dp[0][i - 1]) {
                dp[0][i] = true;
            }
        }

        for (int i = 1 ; i <= n1 ; ++i) {
            for (int j = 1 ; j <= n2 ; ++j) {
                dp[i][j] = ((s3[i + j - 1] == s1[i - 1]) && dp[i - 1][j]) ||
                           ((s3[i + j - 1] == s2[j - 1]) && dp[i][j - 1]);
            }
        }

        return dp[n1][n2];
    }
};
```