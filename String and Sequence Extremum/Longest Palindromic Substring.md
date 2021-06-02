
# Problem
### LeetCode 5. Longest Palindromic Substring
https://leetcode.com/problems/longest-palindromic-substring

# Solution
```c++
class Solution {
public:
    string longestPalindrome(string s) {

        /**
         *  TC: O(S^2), where
         *      S is the length of string s
         *
         *  SC: O(S^2)
         *
         *  palin[i][j]: Whether the substring starting at the index i and
         *               ending at the index j is palindromic.
         *
         *  palin[i][j] = s[i] == s[j] && palin[i + 1][j - 1]
         *
         *  Since the beginning and the ending offsets already show the
         *  length of this palindromic substring, we do not need an extra
         *  data structure to keep track of the length information.
         */

        int n = s.length();

        vector<vector<bool>> dp(n, vector<bool>(n));
        int len = 1, bgn = 0;

        for (int i = 0 ; i < n ; ++i) {
            dp[i][i] = true;
            if (i < n - 1) {
                dp[i][i + 1] = s[i] == s[i + 1];
                if (dp[i][i + 1]) {
                    len = 2;
                    bgn = i;
                }
            }
        }

        for (int l = 3 ; l <= n ; ++l) {
            for (int i = 0, j = i + l - 1 ; i <= n - l ; ++i, ++j) {
                dp[i][j] = dp[i + 1][j - 1] && (s[i] == s[j]);
                if (dp[i][j]) {
                    len = l;
                    bgn = i;
                }
            }
        }

        return s.substr(bgn, len);
    }
};
```