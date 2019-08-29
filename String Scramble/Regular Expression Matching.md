
# Problem
### LintCode 154. Regular Expression Matching
https://www.lintcode.com/problem/regular-expression-matching/description

# Solution
```c++
class Solution {
public:
    /**
     * @param s: A string
     * @param p: A string includes "." and "*"
     * @return: A boolean
     */
    bool isMatch(string &s, string &p) {
        // write your code here

        /**
         * dp[i][j]: Whether the substring of s ending at the index i can be
         *           matched by the subpattern of p ending at the index j.
         *
         *            | if s[i] == p[j] || p[j] == '.'        , dp[i - 1][j - 1]
         *            |
         * dp[i][j] = | if p[j] == '*'
         *            | |  s[i] == p[j - 1] || p[j - 1] == '.', dp[i - 1][j]
         *            | |  No plan to match                   , dp[i][j - 2]
         *            |
         *            | Otherwise                             , false
         */

        int len_s = s.length();
        int len_p = p.length();

        std::vector<std::vector<bool>>
            dp(len_s + 1, std::vector<bool>(len_p + 1, false));
        dp[0][0] = true;

        for (int i = 1 ; i <= len_p ; ++i) {
            if (i >= 2 && p[i - 1] == '*') {
                dp[0][i] = dp[0][i - 2];
            }
        }

        for (int i = 1 ; i <= len_s ; ++i) {
            for (int j = 1 ; j <= len_p ; ++j) {
                if (s[i - 1] == p[j - 1] || p[j - 1] == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                if (j >= 2 && p[j - 1] == '*') {
                    dp[i][j] = dp[i][j - 2];
                    if (s[i - 1] == p[j - 2] || p[j - 2] == '.') {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }

        return dp[len_s][len_p];
    }
};
```