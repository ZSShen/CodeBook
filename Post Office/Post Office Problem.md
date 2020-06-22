
# Problem
### LeetCode 1478. Allocate Mailboxes
https://leetcode.com/problems/allocate-mailboxes/

# Solution
```c++
class Solution {
public:
    int minDistance(vector<int>& houses, int k) {

        /**
         * dp[i][j]: The minimum cost to build i mailboxes to serve the first
         *           j houses.
         *
         * cost[i][j]: The minimum cost to build a mailbox to serve the
         *             houses within the range i and j.
         *
         * dp[i][j] =     MIN   {dp[i - 1][k] + cost[k + 1][j]}
         *            (i-1)<=k<j
         */

        int n = houses.size();

        sort(houses.begin(), houses.end());

        vector<vector<int>> cost(n, vector<int>(n, 0));
        for (int i = 0 ; i < n ; ++i) {
            for (int j = i ; j < n ; ++j) {
                int m = houses[(i + j) / 2];
                int c = 0;
                for (int k = i ; k <= j ; ++k) {
                    c += abs(m - houses[k]);
                }
                cost[i][j] = c;
            }
        }

        vector<vector<int>> dp(k, vector<int>(n, INT_MAX));
        for (int i = 0 ; i < n ; ++i) {
            dp[0][i] = cost[0][i];
        }

        for (int i = 1 ; i < k ; ++i) {
            for (int j = i ; j < n ; ++j) {
                for (int h = 0 ; h < j ; ++h) {
                    if (h < i - 1) {
                        continue;
                    }
                    dp[i][j] = min(
                        dp[i][j],
                        dp[i - 1][h] + cost[h + 1][j]);
                }
            }
        }

        return dp[k - 1][n - 1];
    }
};
```
