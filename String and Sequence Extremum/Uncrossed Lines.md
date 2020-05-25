
# Problem
### LeetCode 1035. Uncrossed Lines
https://leetcode.com/problems/uncrossed-lines/

# Solution
```c++
class Solution {
public:
    int maxUncrossedLines(vector<int>& A, vector<int>& B) {

        /**
            dp[i][j]: The max number of uncrossing lines produced by using
            the first i numbers of A and the first j numbers of B.


            dp[i][j] = MAX | if A[i] == B[j], dp[i - 1][j - 1] + 1
                           | Otherwise.     , dp[i][j - 1]
                                            , dp[i - 1][j]
                                            , dp[i - 1][j - 1]
        */

        int na = A.size();
        int nb = B.size();
        vector<vector<int>> dp(na + 1, vector<int>(nb + 1, 0));

        for (int i = 1 ; i <= na ; ++i) {
            for (int j = 1 ; j <= nb ; ++j) {
                int c = dp[i - 1][j - 1];
                if (A[i - 1] == B[j - 1]) {
                    ++c;
                }

                c = max(c, dp[i - 1][j]);
                c = max(c, dp[i][j - 1]);
                dp[i][j] = c;
            }
        }

        return dp[na][nb];
    }
};
```