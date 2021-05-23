
# Problem
### LeetCode 72. Edit Distance
https://leetcode.com/problems/edit-distance

# Solution
```c++
class Solution {
public:
    int minDistance(string s, string t) {

        /**
         * dp[i][j]: The minimum costs to transform the prefix of A ending at
         *           the index i to the prefix of B ending at the index j.
         *
         *  dp[i][j] = | if A[i] == B[j], dp[i - 1][j - 1]
         *             | otherwise      , MIN | 1 + dp[i - 1][j - 1], replace A[i].
         *                                    | 1 + dp[i][j - 1]    , insert a letter.
         *                                    | 1 + dp[i - 1][j]    , delete a letter.
         */

        int ns = s.length();
        int nt = t.length();

        vector<vector<int>> dp(ns + 1, vector<int>(nt + 1));

        for (int i = 0 ; i <= nt ; ++i) {
            dp[0][i] = i;
        }
        for (int i = 0 ; i <= ns ; ++i) {
            dp[i][0] = i;
        }

        for (int i = 1 ; i <= ns ; ++i) {
            for (int j = 1 ; j <= nt ; ++j) {
                if (s[i - 1] == t[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    int opt = dp[i - 1][j - 1] + 1;
                    opt = min(opt, dp[i][j - 1] + 1);
                    opt = min(opt, dp[i - 1][j] + 1);
                    dp[i][j] = opt;
                }
            }
        }

        return dp[ns][nt];
    }
};
```