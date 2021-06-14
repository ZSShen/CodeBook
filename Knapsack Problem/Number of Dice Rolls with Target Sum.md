
# Problem
### LeetCode 1155. Number of Dice Rolls With Target Sum
https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/

# Solution
```c++
class Solution {
public:
    int numRollsToTarget(int d, int f, int target) {

        /**
         *  TC: O(D * F * T), where
         *      D is the number of dices
         *      F is the number of faces
         *      T it the target amount
         *
         *  SC: O(D * T)
         *
         *  dp[i][j]: The number of ways to sum up to j using the first i dices.
         *
         *  dp[i][j] =   SUM { dp[i - 1][j - k] | j >= k }
         *             0<=k<=f
         */

        long mod = 1e9 + 7;
        vector<vector<long>> dp(d + 1, vector<long>(target + 1));
        dp[0][0] = 1;

        for (int i = 1 ; i <= d ; ++i) {
            for (int j = 1 ; j <= f ; ++j) {
                for (int k = j ; k <= target ; ++k) {
                    dp[i][k] = (dp[i][k] + dp[i - 1][k - j]) % mod;
                }
            }
        }

        return dp[d][target];
    }
};
```