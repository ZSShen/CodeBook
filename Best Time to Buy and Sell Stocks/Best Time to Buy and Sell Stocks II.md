
# Problem
### LintCode 150. Best Time to Buy and Sell Stocks II
https://www.lintcode.com/problem/best-time-to-buy-and-sell-stock-ii/description

# Solution
```c++
class Solution {
public:
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    int maxProfit(vector<int> &prices) {
        // write your code here

        /**
         * 1 7 2 4 5 6 1
         *
         *   *
         *   *       *
         *   *     * *
         *   *   * * *
         *   *   * * *
         *   * * * * *
         * * * * * * * *
         * _____________
         *
         * Objective: Aggregate all the ascending segments.
         *
         *      Segments: (0, 1), (2, 6)
         *      Value   : 6     , 4
         */

        int n = prices.size();
        if (n == 0) {
            return 0;
        }

        int ans = 0;
        int bgn = 0, end = 1;

        while (end < n) {

            // Find the ending position of the current ascending segment.
            if (prices[end] < prices[end - 1]) {
                ans += prices[end - 1] - prices[bgn];
                bgn = end;
            }
            ++end;
        }
        ans += prices[end - 1] - prices[bgn];

        return ans;
    }
};
```