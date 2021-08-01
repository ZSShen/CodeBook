
# Problem
### LeetCode 123. Best Time to Buy and Sell Stock III
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii

# Solution
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {

        /**
         *  TC: O(N), where
         *      N is the number of days
         *
         *  SC: O(1)
         *
            dp[i][2][SOLD] = MAX | dp[i - 1][2][SOLD]
                                 | dp[i - 1][2][HOLD] + prices[i]

            dp[i][2][HOLD] = MAX | dp[i - 1][2][HOLD]
                                 | dp[i - 1][1][SOLD] - prices[i]

            dp[i][1][SOLD] = MAX | dp[i - 1][1][SOLD]
                                 | dp[i - 1][1][HOLD] + prices[i]

            dp[i][1][HOLD] = MAX | dp[i - 1][1][HOLD]
                                 | dp[i - 1][0][SOLD] - prices[i]

            dp_2_sold, dp_2_hold
            dp_1_sold, dp_1_hold

            sold means not holding anything in hand.

            dp_2_sold = dp_1_sold = 0
            dp_2_hold = dp_1_hold = INT_MIN (impossible to do so)
        */

        int dp_2_sold = 0, dp_1_sold = 0;
        int dp_2_hold = INT_MIN, dp_1_hold = INT_MIN;

        for (int price : prices) {
            dp_1_hold = max(dp_1_hold, - price);
            dp_1_sold = max(dp_1_sold, dp_1_hold + price);
            dp_2_hold = max(dp_2_hold, dp_1_sold - price);
            dp_2_sold = max(dp_2_sold, dp_2_hold + price);
        }

        return dp_2_sold;
    }
};
```