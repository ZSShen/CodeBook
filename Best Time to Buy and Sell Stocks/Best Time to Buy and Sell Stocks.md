
# Problem
### LeetCode 121. Best Time to Buy and Sell Stock
https://leetcode.com/problems/best-time-to-buy-and-sell-stock

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
         */

        int n = prices.size();
        if (n < 2) {
            return 0;
        }

        int ans = 0;
        int buy = prices[0];

        for (int i = 1 ; i < n ; ++i) {
            ans = max(ans, prices[i] - buy);
            buy = min(buy, prices[i]);
        }

        return ans;
    }
};
```