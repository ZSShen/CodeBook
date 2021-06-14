
# Problem
### LeetCode 322. Coin Change
https://leetcode.com/problems/coin-change

# Solution
```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {

        /**
         *  TC: O(N * C), where
         *      N is the number of coins
         *      C is the given amount
         *
         *  SC: O(C)
         *
         *  dp[i]: The minimum number of coins that make i dollars.
         *
         *  dp[i] = MIN { dp[i - coins[j] | 0 <= j < n and i >= coins[j] } + 1
         */

        vector<int> dp(amount + 1, INT_MAX);
        dp[0] = 0;

        for (int c : coins) {
            for (int i = c ; i <= amount ; ++i) {
                if (dp[i - c] == INT_MAX) {
                    continue;
                }
                dp[i] = min(dp[i], dp[i - c] + 1);
            }
        }

        return dp[amount] < INT_MAX ? dp[amount] : -1;
    }
};
```