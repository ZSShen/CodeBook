
# Problem
### LeetCode 10. Regular Expression Matching
https://leetcode.com/problems/regular-expression-matching

# Solution
```c++
class Solution {
public:
    bool isMatch(string s, string p) {

        /**
         *  TC: O(S * P), where
         *      S is the length of string S
         *      P is the length of pattern P
         *
         *  SC: O(S * P)
         *
         *  dp[i][j]: Whether the prefix of S ending at offset i can
         *            be matched by the prefix of P ending at offset j.
         *
         *             | if s[i] == p[j] || p[j] == '.'        , dp[i - 1][j - 1]
         *             |
         *  dp[i][j] = | if p[j] == '*'
         *             | |  s[i] == p[j - 1] || p[j - 1] == '.', dp[i - 1][j]
         *             | |  No plan to match                   , dp[i][j - 2]
         *             |
         *             | Otherwise                             , false
         */

        int ls = s.length();
        int lp = p.length();

        vector<vector<bool>> dp(ls + 1, vector<bool>(lp + 1));
        dp[0][0] = true;

        // dp[0][0...lp]
        // S:
        // P: a*b*, .*c*
        // The reson why we do not assign dp[0][i] = true: *C**
        for (int i = 2 ; i <= lp ; ++i) {
            if (p[i - 1] == '*') {
                dp[0][i] = dp[0][i - 2];
            }
        }

        for (int i = 1 ; i <= ls ; ++i) {
            for (int j = 1 ; j <= lp ; ++j) {
                if (s[i - 1] == p[j - 1] || p[j - 1] == '.') {
                    dp[i][j] = dp[i - 1][j - 1];

                } else if (j >= 2 && p[j - 1] == '*') {
                    // By default, no plan to match.
                    dp[i][j] = dp[i][j - 2];

                    if (s[i - 1] == p[j - 2] || p[j - 2] == '.') {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }

        return dp[ls][lp];
    }
};
```