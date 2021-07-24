
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
        dp[0] = 0;
        for (int day : days) {
            dp[day] = 0;
        }

        for (int i = 1 ; i <= n ; ++i) {
            if (dp[i] == -1) {
                dp[i] = dp[i - 1];
                continue;
            }

            dp[i] = dp[i - 1] + costs[0];
            dp[i] = min(dp[i], dp[max(0, i - 7)] + costs[1]);
            dp[i] = min(dp[i], dp[max(0, i - 30)] + costs[2]);
        }

        return dp[n];
    }
};
```