
# Problem
### LintCode 125 Backpack II
https://www.lintcode.com/problem/backpack-ii/description

# Solution
```c++
class Solution {
public:
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @param V: Given n items with value V[i]
     * @return: The maximum value
     */
    int backPackII(int m, vector<int> &A, vector<int> &V) {
        // write your code here

        /**
         * dp[i][j]: The maximal values the knapsack which can hold j units of
         *           weight can aggregate by using the first i items.
         *
         * dp[i][j] = | W[i] <= j, MAX{ dp[i - 1][j], dp[i - 1][j - W[i]] + V[i] }
         *            | otherwise, dp[i - 1][j]
         */

        int n = A.size();
        if (n == 0) {
            return 0;
        }

        std::vector<std::vector<int>> dp(n + 1, std::vector<int>(m + 1, 0));

        for (int i = 1 ; i <= n ; ++i) {
            for (int j = 1 ; j <= m ; ++j) {

                if (A[i - 1] > j) {
                    dp[i][j] = dp[i - 1][j];
                    continue;
                }

                dp[i][j] = std::max(
                    V[i - 1] + dp[i - 1][j - A[i - 1]], dp[i - 1][j]);
            }
        }

        return dp[n][m];
    }
};
```