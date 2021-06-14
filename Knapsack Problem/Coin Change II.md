
# Problem
### LeetCode 518. Coin Change 2
https://leetcode.com/problems/coin-change-2

# Solution
```c++
class Solution {
public:
    int change(int amount, vector<int>& coins) {

        /**
         *  TC: O(N * C), where
         *      N is number of coins
         *      C is the given amount
         *
         *  SC: O(C)
         *
         *  dp[i]: The number of ways to make i dollars.
         *
         *  dp[i] =  SUM { dp[i - coin[k]] | i >= coin[k] }
         *          0<k<j
         */

        vector<int> dp(amount + 1);
        dp[0] = 1;

        for (int c : coins) {
            for (int i = c ; i <= amount ; ++i) {
                dp[i] += dp[i - c];
            }
        }

        return dp[amount];
    }
};
```