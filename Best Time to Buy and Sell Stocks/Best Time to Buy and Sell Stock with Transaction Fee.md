
# Problem
### LeetCode 714. Best Time to Buy and Sell Stock with Transaction Fee
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee

# Solution
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {

        /**
         *  TC: O(N), where
         *      N is the number of days
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

            dp[i][HOLD] = MAX | dp[i - 1][HOLD]
                              | dp[i - 1][SOLD] - prices[i] - fee

        */

        int dp_sold = 0, dp_hold = INT_MIN;

        for (int price : prices) {
            int old_sold = dp_sold, old_hold = dp_hold;

            dp_sold = max(old_sold, old_hold + price);
            dp_hold = max(old_hold, old_sold - price - fee);
        }

        return dp_sold;
    }
};
```