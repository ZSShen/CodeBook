
# Problem
### LeetCode 1312. Minimum Insertion Steps to Make a String Palindrome
https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/

# Solution
```c++
class Solution {
public:
    int minInsertions(string s) {

        /**
            dp[i][j]: The minimum number of steps to make the substring s(i, j) palindromic.

            dp[i][j] = | if s[i] == s[j], dp[i + 1][j - 1]
                       | otherwise,       1 + MIN{ dp[i][j - 1], dp[i + 1][j]}
        */

        int n = s.length();
        vector<vector<int>> dp(n, vector<int>(n, 0));

        for (int i = 0 ; i < n - 1 ; ++i) {
            if (s[i] != s[i + 1]) {
                dp[i][i + 1] = 1;
            }
        }

        for (int l = 3 ; l <= n ; ++l) {
            for (int i = 0, j = i + l - 1 ; i <= n - l ; ++i, ++j) {
                if (s[i] == s[j]) {
                    dp[i][j] = dp[i + 1][j - 1];
                } else {
                    dp[i][j] = 1 + std::min(dp[i][j - 1], dp[i + 1][j]);
                }
            }
        }

        return dp[0][n - 1];
    }
};
```