
# Problem
### LintCode 564 Combination Sum IV
https://www.lintcode.com/problem/combination-sum-iv/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: an integer array and all positive numbers, no duplicates
     * @param target: An integer
     * @return: An integer
     */
    int backPackVI(vector<int> &nums, int target) {
        // write your code here

        /**
         *  TC: O(N * T), where
         *      N is the number of elements
         *      T is the given target
         *
         *  SC: O(T)
         *
         *
         *  dp[i]: The number of ways to sum up to i using any combination of numbers.
         *
         *  dp[i] =  SUM { dp[i - nums[j] | i >= nums[j]}
         *          0<=j<n
         *
         *  *Initial case:
         *  We have one way to compose 0 — using nothing.
         *  dp[0] = 1
         */

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        vector<int> dp(target + 1);
        dp[0] = 1;

        for (int i = 1 ; i <= target ; ++i) {
            for (int num : nums) {
                if (num > i) {
                    continue;
                }
                dp[i] += dp[i - num];
            }
        }

        return dp[target];
    }
};
```