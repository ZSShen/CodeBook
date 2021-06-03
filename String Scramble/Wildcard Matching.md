
# Problem
### LeetCode 44. Wildcard Matching
https://leetcode.com/problems/wildcard-matching

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
         *  dp[i][j]: Whether the prefix of S ending at the offset i can
         *            be matched by the prefix of P ending at offset j.
         *
         *             | if s[i] == p[j] || p[j] == '?', dp[i - 1][j - 1]
         *  dp[i][j] = | if p[j] == '*'                , dp[i - 1][j] || dp[i][j- 1]
         *             | otherwise                     , false
         */

        int ls = s.length();
        int lp = p.length();

        vector<vector<bool>> dp(ls + 1, vector<bool>(lp + 1));
        dp[0][0] = true;

        // dp[0][0...lp]
        // S:
        // P: *, **, ***A

        for (int i = 1 ; i <= lp ; ++i) {
            if (p[i - 1] != '*') {
                break;
            }
            dp[0][i] = true;
        }

        for (int i = 1 ; i <= ls ; ++i) {
            for (int j = 1 ; j <= lp ; ++j) {
                if (s[i - 1] == p[j - 1] || p[j - 1] == '?') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p[j - 1] == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                }
            }
        }

        return dp[ls][lp];
    }
};
```