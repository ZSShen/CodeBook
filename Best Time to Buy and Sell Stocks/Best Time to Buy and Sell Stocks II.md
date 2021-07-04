
# Problem
### LeetCode 122. Best Time to Buy and Sell Stock II
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii

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
         *      7 1 5 3 6 4
         *
         *      *
         *      *       *
         *      *   *   *
         *      *   *   * *
         *      *   * * * *
         *      *   * * * *
         *      * * * * * *
         *
         *  Segments: (1, 2), (3, 4)
         *  profits : 4     , 3
         */

        int n = prices.size();
        int ans = 0;

        for (int i = 1 ; i < n ; ++i) {
            if (prices[i] > prices[i - 1]) {
                ans += prices[i] - prices[i - 1];
            }
        }

        return ans;
    }
};
```