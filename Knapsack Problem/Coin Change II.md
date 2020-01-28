
# Problem
### LintCode 740. Coin Change 2
https://www.lintcode.com/problem/coin-change-2/description

# Solution
```c++
class Solution {
public:
    /**
     * @param amount: a total amount of money amount
     * @param coins: the denomination of each coin
     * @return: the number of combinations that make up the amount
     */
    int change(int amount, vector<int> &coins) {
        // write your code here

        /**
         * dp[i]: The number of ways to make i dollars.
         *
         * dp[i] =  SUM { dp[i - coin[k]] | i >= coin[k] }
         *         0<k<j
         */

        vector<int> dp(amount + 1, 0);
        dp[0] = 1;

        for (int coin : coins) {
            for (int i = 1 ; i <= amount ; ++i) {
                if (coin > i) {
                    continue;
                }
                dp[i] += dp[i - coin];
            }
        }

        return dp[amount];
    }
};
```