
# Problem
### LeetCode 188. Best Time to Buy and Sell Stock IV
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv

# Solution
```c++
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {

        /**
         *  TC: O(N * K), wherew
         *      N is the number of days
         *
         *  SC: O(K)
         *
            dp[i][k][SOLD]: The maximum profits we can acquire
                    if we hold nothing after k purchases (transactions)
                    at the end of the ith day.

            dp[i][k][HOLD]: The maximum profits we can acquire
                    if we still hold the stock after k purchases (transactions)
                    at the end of the ith day.


            dp[i][k][SOLD] = MAX | dp[i - 1][k][SOLD]x`
                                    , rest for today.

                                 | dp[i - 1][k][HOLD] + prices[i]
                                    , sell the stock today.

            dp[i][k][HOLD] = MAX | dp[i - 1][k][HOLD]
                                    , rest for today.

                                 | dp[i - 1][k - 1][SOLD] - prices[i]
                                    , make the kth purchase today.

            SOLD: holding nothing in hand

            dp[-1][k][SOLD] = dp[i][0][SOLD] = 0
            dp[-1][k][HOLD] = dp[i][0][HOLD] = INT_MIN (impossible to do so)
        */

        int n = prices.size();

        if (k >= n / 2) {
            // Solve using greedy approach.
            int ans = 0;
            for (int i = 1 ; i < n ; ++i) {
                if (prices[i] > prices[i - 1]) {
                    ans += prices[i] - prices[i - 1];
                }
            }
            return ans;
        }

        vector<int> dp_sold(k + 1);
        vector<int> dp_hold(k + 1, INT_MIN);

        for (int price : prices) {
            for (int j = 1 ; j <= k ; ++j) {
                dp_hold[j] = max(dp_hold[j], dp_sold[j - 1] - price);
                dp_sold[j] = max(dp_sold[j], dp_hold[j] + price);
            }
        }

        return dp_sold[k];
    }
};
```