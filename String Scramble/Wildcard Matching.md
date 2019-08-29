
# Problem
### LintCode 192. Wildcard Matching
https://www.lintcode.com/problem/wildcard-matching/description

# Solution
```c++
class Solution {
public:
    /**
     * @param s: A string
     * @param p: A string includes "?" and "*"
     * @return: is Match?
     */
    bool isMatch(string &s, string &p) {
        // write your code here

        /**
         * dp[i][j]: Whether the substring of s ending at the index i can
         *           be matched by the subpattern of p ending at the index j.
         *
         *            | if s[i] == p[j] || p[j] == '?', dp[i - 1][j - 1]
         * dp[i][j] = | if p[j] == '*'                , dp[i - 1][j] || dp[i][j- 1]
         *            | otherwise                     , false
         */

        int len_s = s.length();
        int len_p = p.length();

        std::vector<std::vector<bool>>
            dp(len_s + 1, std::vector<bool>(len_p + 1, false));
        dp[0][0] = true;

        for (int i = 1 ; i <= len_p ; ++i) {
            if (p[i - 1] != '*') {
                break;
            }
            dp[0][i] = true;
        }

        for (int i = 1 ; i <= len_s ; ++i) {
            for (int j = 1 ; j <= len_p ; ++j) {
                if (s[i - 1] == p[j - 1] || p[j - 1] == '?') {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                if (p[j - 1] == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                }
            }
        }

        return dp[len_s][len_p];
    }
};
```