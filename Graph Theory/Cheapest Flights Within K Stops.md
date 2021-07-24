
# Problem
### LeetCode 787. Cheapest Flights Within K Stops
https://leetcode.com/problems/cheapest-flights-within-k-stops

# Solution
```c++
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {

        /**
         *  TC: O(K * n), where
         *      n is the number of cities
         *
         *  SC: O(K * n)
         *
            dp[i][j]: The minimum cost to reach city j by taking i hops.

            dp[i][j] = MIN { dp[i - 1][k] + dist[k][j] | k != j }
                      0<=k<n
        */

        vector<vector<int>> dp(K + 2, vector<int>(n, INT_MAX / 2));
        for (int i = 0 ; i <= K + 1 ; ++i) {
            dp[i][src] = 0;
        }

        for (int i = 1 ; i <= K + 1 ; ++i) {
            for (const auto& f : flights) {
                int u = f[0];
                int v = f[1];
                int w = f[2];
                if (dp[i - 1][u] + w < dp[i][v]) {
                    dp[i][v] = dp[i - 1][u] + w;
                }
            }
        }

        return dp[K + 1][dst] < INT_MAX / 2 ? dp[K + 1][dst] : -1;
    }
};
```