
# Problem
### LeetCode 1062. Longest Repeating Substring
https://leetcode.com/problems/longest-repeating-substring/

# Solution
```c++
class Solution {
public:
    int longestRepeatingSubstring(string S) {

        /**
         *  TC: O(S^2), where
         *      S is the length of string s
         *
         *  SC: O(S^2)
         *
         *
         *  dp[i][j]: The length of the longest common substring shared by the
         *            substring ending at the index i and the other one ending
         *            at the index j.
         *
         *  dp[i][j] = | if s[i] == s[j] and j < i,  1 + dp[i - 1][j - 1]
         *             | else                     ,  0
         *
         *  example: c d e d a a a
         *
         *       i
         *   j
         *       0 c d e d a a a
         *       0 0 0 0 0 0 0 0
         *   0 0   0 0 0 0 0 0 0
         *   c 0     0 0 0 0 0 0
         *   d 0       0 1 0 0 0
         *   e 0         0 0 0 0
         *   d 0           0 0 0
         *   a 0             1 1
         *   a 0               2
         *   a 0
         *
         */

        int n = S.length();
        vector<vector<int>> dp(n + 1, vector<int>(n + 1));

        int ans = 0;

        for (int i = 1 ; i < n ; ++i) {
            for (int j = 0 ; j < i ; ++j) {
                if (S[i] == S[j]) {
                    dp[i + 1][j + 1] = 1 + dp[i][j];
                    ans = max(ans, dp[i + 1][j + 1]);
                }
            }
        }

        return ans;
    }
};
```