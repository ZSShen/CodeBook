
# Problem
### LeetCode 983. Minimum Cost For Tickets
https://leetcode.com/problems/minimum-cost-for-tickets/

# Solution
```c++
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {

        /*
            dp[i]: The minimum cost till the ith day.

            dp[i] = | dp[i - 1]                  ,we don't need to travel in the ith day.
                    |     | cost[D] + dp[i - 1]
                    | MIN | cost[W] + dp[i - 7]  ,we must travel in the ith day.
                    |     | cost[M] + dp[i - 30]
        */

        int n = days.back();

        vector<int> dp(n + 1, -1);
        for (int day : days) {
            dp[day] = 0;
        }

        dp[0] = 0;
        for (int i = 1 ; i <= n ; ++i) {
            if (dp[i] == -1) {
                dp[i] = dp[i - 1];
                continue;
            }

            int cost = dp[i - 1] + costs[0];
            cost = std::min(cost, costs[1] + dp[std::max(0, i - 7)]);
            cost = std::min(cost, costs[2] + dp[std::max(0, i - 30)]);
            dp[i] = cost;
        }

        return dp[n];
    }
};
```