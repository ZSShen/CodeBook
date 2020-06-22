
# Problem
### LintCode 1278. Palindrome Partitioning III
https://leetcode.com/problems/palindrome-partitioning-iii/

# Solution
```c++
class Solution {
public:
    int palindromePartition(string s, int K) {

        /**
            dp[i][k]: The minimum cost to convert each of the k substrings
                      of the string with length i to palindrome.

            dp[i][k] =   MIN { dp[j][k - 1] + cost[j + 1][i] }
                       0<=j<i
        */

        int n = s.length();

        vector<vector<int>> cost(n, vector<int>(n, 0));
        for (int l = 2 ; l <= n ; ++l) {
            for (int i = 0, j = i + l - 1 ; i <= n - l ; ++i, ++j) {
                cost[i][j] = (s[i] != s[j]) + cost[i + 1][j - 1];
            }
        }

        vector<vector<int>> dp(n, vector<int>(K, INT_MAX >> 1));
        for (int i = 0 ; i < n ; ++i) {
            dp[i][0] = cost[0][i];

            for (int k = 1 ; k < K ; ++k) {
                for (int j = 0 ; j < i ; ++j) {
                    dp[i][k] = min(dp[i][k], dp[j][k - 1] + cost[j + 1][i]);
                }
            }
        }

        return dp[n - 1][K - 1];
    }
};
```