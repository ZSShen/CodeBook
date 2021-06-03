
# Problem
### LeetCode 115. Distinct Subsequences
https://leetcode.com/problems/distinct-subsequences

# Solution
```c++
class Solution {
public:
    int numDistinct(string s, string t) {

        /**
         *  TC: O(S * T), where
         *      S is the length of string s
         *      T is the length of string t
         *
         *  SC: O(S * T)
         *
         *  dp[i][j]: The number of distinct ways to produce the prefix of T
         *            ending at the jth position by removing any character
         *            of the prefix of S ending at the ith position.
         *
         *  dp[i][j] = | if S[i] == T[j], dp[i - 1][j - 1] + dp[i - 1][j]
         *             | otherwise      , dp[i - 1][j]
         *
         *    0 r a b b b i t
         *  0 1 1 1 1 1 1 1 1
         *  r 0 1 1 1 1 1 1 1
         *  a 0 0 1 1 1 1 1 1
         *  b 0 0 0 1 2 3 3 3
         *  b 0 0 0 0 1 3 3 3
         *  i 0 0 0 0 0 0 3 3
         *  t 0 0 0 0 0 0 0 3
         */

        int ns = s.length();
        int nt = t.length();

        long mod = 1e9 + 7;
        vector<vector<long>> dp(ns + 1, vector<long>(nt + 1));

        for (int i = 0 ; i <= ns ; ++i) {
            dp[i][0] = 1;
        }

        for (int i = 1 ; i <= ns ; ++i) {
            for (int j = 1 ; j <= nt ; ++j) {
                dp[i][j] = dp[i - 1][j];
                if (s[i - 1] == t[j - 1]) {
                    dp[i][j] += dp[i - 1][j - 1];
                }
                dp[i][j] %= mod;
            }
        }

        return dp[ns][nt];
    }
};
```