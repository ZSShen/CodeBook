
# Problem
### LeetCode 1062. Longest Repeating Substring
https://leetcode.com/problems/longest-repeating-substring/

# Solution
```c++
class Solution {
public:
    int longestRepeatingSubstring(string S) {

        /**
            dp[i][j]: The length of the longest common substring
            shared by the substring ending at offset i and the
            other one ending at offset j.

            dp[i][j] = | s[i] != s[j], 0
                       |
                       | otherwise   , dp[i - 1][j - 1] + 1
        */

        int n = S.length();
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

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