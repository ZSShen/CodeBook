
# Problem
### LeetCode 1155. Number of Dice Rolls With Target Sum
https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/

# Solution
```c++
class Solution {
public:
    int numRollsToTarget(int d, int f, int target) {

        /*
        dp[i][j]: The number of ways to sum up to j using the first i dices.

        dp[i][j] =   SUM { dp[i - 1][j - k] | j >= k }
                   0<=k<=f
        */

        vector<vector<long>> dp(d + 1, vector<long>(target + 1, 0));
        dp[0][0] = 1;

        for (int i = 1 ; i <= d ; ++i) {
            for (int j = 1 ; j <= target ; ++j) {
                long sum = 0;
                for (int k = 1 ; k <= f ; ++k) {
                    if (k > j) {
                        continue;
                    }
                    sum += dp[i - 1][j - k];
                    sum = sum % 1000000007;
                }
                dp[i][j] = sum;
            }
        }

        return dp[d][target];
    }
};
```