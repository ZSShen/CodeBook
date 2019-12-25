
# Problem
### LintCode 669. Coin Change
https://www.lintcode.com/problem/coin-change/description

# Solution
```c++
class Solution {
public:
    /**
     * @param coins: a list of integer
     * @param amount: a total amount of money amount
     * @return: the fewest number of coins that you need to make up
     */
    int coinChange(vector<int> &coins, int amount) {
        // write your code here

        /**
         * dp[i]: The minimum number of coins that make i dollars.
         *
         * dp[i] = MIN { dp[i - coins[j] | 0 <= j < n and i >= coins[j] } + 1
         */

        int n = coins.size();
        if (n == 0) {
            return -1;
        }

        std::vector<int> dp(amount + 1, INT_MAX);
        dp[0] = 0;

        for (int i = 1 ; i <= amount ; ++i) {
            int min = INT_MAX;
            for (int coin : coins) {
                if (coin > i) {
                    continue;
                }
                min = std::min(min, dp[i - coin]);
            }

            if (min < INT_MAX) {
                dp[i] = min + 1;
            }
        }

        return dp[amount] != INT_MAX ? dp[amount] : -1;
    }
};
```