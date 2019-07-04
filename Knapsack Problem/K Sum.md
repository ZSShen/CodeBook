
# Problem
### LintCode 89 K Sum
https://www.lintcode.com/problem/k-sum/description

# Solution
```c++
class Solution {
public:
    /**
     * @param A: An integer array
     * @param k: A positive integer (k <= length(A))
     * @param target: An integer
     * @return: An integera
     */
    int kSum(vector<int> &A, int k, int target) {
        // write your code here

        /**
         * dp[i][j][h]: The number of ways to use j integers from the first i
         *              integers to compose h.
         *
         * dp[i][j][h] = | A[i] <= h, dp[i - 1][j][h] + dp[i - 1][j - 1][h - A[i]]
         *               | Otherwise, dp[i - 1][j][h]
         */

        int n = A.size();
        if (n == 0) {
            return 0;
        }

        std::vector<std::vector<std::vector<int>>>
            dp(n + 1, std::vector<std::vector<int>>(
                k + 1, std::vector<int>(target + 1, 0)));

        for (int i = 0 ; i <= n ; ++i) {
            dp[i][0][0] = 1;
        }

        for (int i = 1 ; i <= n ; ++i) {
            for (int j = 1 ; j <= k && j <= i ; ++j) {
                for (int h = 1 ; h <= target ; ++h) {

                    if (A[i - 1] > h) {
                        dp[i][j][h] = dp[i - 1][j][h];
                        continue;
                    }

                    dp[i][j][h] = dp[i - 1][j][h] + dp[i - 1][j - 1][h - A[i - 1]];
                }
            }
        }

        return dp[n][k][target];
    }
};
```