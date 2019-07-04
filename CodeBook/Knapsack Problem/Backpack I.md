
# Problem
### LintCode 92 Backpack
https://www.lintcode.com/problem/backpack/description


# Solution
```c++
class Solution {
public:
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    int backPack(int m, vector<int> &A) {
        // write your code here

        /**
         * dp[i][j]: The maximal size the knapsack which can hold j units of
         *           weight can aggregate by using the first i items.
         *
         * dp[i][j] = | A[i] <= j, MAX{ dp[i - 1][j], dp[i - 1][j - A[i]] + A[i] }
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

                dp[i][j] =
                    std::max(dp[i - 1][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
            }
        }

        return dp[n][m];
    }
};
```