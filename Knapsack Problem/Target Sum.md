
# Problem
### LintCode 1208. Target Sum
https://www.lintcode.com/problem/target-sum/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: the given array
     * @param s: the given target
     * @return: the number of ways to assign symbols to make sum of integers equal to target S
     */
    int findTargetSumWays(vector<int> &nums, int s) {
        // Write your code here

        /**
         * dp[i][j]: The number of ways to sum up to j using the first i numbers.
         *
         * dp[i][j] = dp[i - 1][j - nums[i]] + dp[i - 1][j + nums[i]]
         *
         * (For the second dimension, we can use hash table because its value
         *  range is discrete.)
         */

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        vector<unordered_map<int, int>> dp(n);

        dp[0][nums[0]] += 1;
        dp[0][-nums[0]] += 1;

        for (int i = 1 ; i < n ; ++i) {
            for (auto& pair : dp[i - 1]) {
                int sum = pair.first;
                int way = pair.second;
                dp[i][sum + nums[i]] += way;
                dp[i][sum - nums[i]] += way;
            }
        }

        return dp[n - 1][s];
    }
};
```