
# Problem
### LintCode 163. Unique Binary Search Trees
https://www.lintcode.com/problem/unique-binary-search-trees/description

# Solution
```c++
class Solution {
public:
    /**
     * @param n: An integer
     * @return: An integer
     */
    int numTrees(int n) {
        // write your code here

        /**
         * dp[i][j]: The number of unique binary search trees generated by
         *           the nodes starting from the ith node to the jth node.
         *
         * dp[i][j] =   SUM { dp[i][k - 1] * dp[k + 1][j] }
         *            i<=k<=j
         */

        if (n <= 1) {
            return 1;
        }

        if (n == 2) {
            return 2;
        }

        std::vector<std::vector<int>> dp(n, std::vector<int>(n, 0));
        for (int i = 0 ; i < n - 1 ; ++i) {
            dp[i][i] = 1;
            dp[i][i + 1] = 2;
        }
        dp[n - 1][n - 1] = 1;

        for (int l = 3 ; l <= n ; ++l) {
            for (int i = 0, j = i + l - 1 ; i <= n - l ; ++i, ++j) {
                for (int k = i ; k <= j ; ++k) {
                    int left = (k > i) ? dp[i][k - 1] : 1;
                    int rght = (k < j) ? dp[k + 1][j] : 1;
                    dp[i][j] += left * rght;
                }
            }
        }

        return dp[0][n - 1];
    }
};
```