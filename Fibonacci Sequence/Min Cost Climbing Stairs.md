# Problem

### LeetCode 746. Min Cost Climbing Stairs
https://leetcode.com/problems/min-cost-climbing-stairs

# Solution
```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {

        /**
         *  TC: O(N), where
         *      N is the number of cells
         *
         *  SC: O(N)
         *
         *  dp[i]: The minimum cost to reach the ith hop.
         *
         *  dp[i] = MIN | dp[i - 1] + cost[i - 1]
         *              | dp[i - 2] + cost[i - 2]
         */

        int n = cost.size();
        vector<int> dp(n + 1);

        for (int i = 2 ; i <= n ; ++i) {
            dp[i] = min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
        }
        return dp[n];
    }
};
```
