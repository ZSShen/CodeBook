
# Problem
### LintCode 563 Backpack V
https://www.lintcode.com/problem/backpack-v/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: an integer array and all positive numbers
     * @param target: An integer
     * @return: An integer
     */
    int backPackV(vector<int> &nums, int target) {
        // write your code here

        /**
         * dp[i][j]: The number of ways to fill the knapsack which can hold j
         *           units of weight using the first i items.
         *
         * dp[i][j] = | nums[i] <= j, dp[i - 1][j] + dp[i - 1][j - nums[i]]
         *            | Otherwise   , dp[i - 1][j]
         */

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        std::vector<std::vector<int>> dp(n + 1, std::vector<int>(target + 1, 0));

        for (int i = 0 ; i <= n ; ++i) {
            dp[i][0] = 1;
        }

        for (int i = 1 ; i <= n ; ++i) {
            for (int j = 1 ; j <= target ; ++j) {

                if (nums[i - 1] > j) {
                    dp[i][j] = dp[i - 1][j];
                    continue;
                }

                dp[i][j] = dp[i - 1][j] + dp[i - 1][j - nums[i - 1]];
            }
        }

        return dp[n][target];
    }
};
```