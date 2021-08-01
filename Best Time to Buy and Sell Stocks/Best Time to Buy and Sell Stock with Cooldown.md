
# Problem
### LeetCode 309. Best Time to Buy and Sell Stock with Cooldown
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown

# Solution
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         *
         *
            dp[i][SOLD]: The maximum profits we can acquire
                if we hold nothing at the end of the ith day

            dp[i][HOLD]: The maximum profits we can acquire
                if we hold the stock at the end of the ith day


            dp[i][SOLD] = MAX | dp[i - 1][SOLD]
                              | dp[i - 1][HOLD] + prices[i]

            dp[i][HOLD] = MAX | ap[i - 1][HOLD]
                              | dp[i - 2][SOLD] - prices[i]
        */

        int dp_sold = 0, dp_sold_pre = 0, dp_hold = INT_MIN;

        for (int price : prices) {
            int old_sold = dp_sold, old_hold = dp_hold;

            dp_sold = max(old_sold, old_hold + price);
            dp_hold = max(old_hold, dp_sold_pre - price);
            dp_sold_pre = old_sold;
        }

        return dp_sold;
    }
};
```