
# Problem
### LeetCode 1269. Number of Ways to Stay in the Same Place After Some Steps
https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps/

# Solution
```c++
class Solution {
public:
    Solution()
        : mod(1e9 + 7)
    { }

    int numWays(int s, int n) {

        /**
         *  TC: O(S * MIN(N, S)), where
         *      S is the number of steps
         *      N is the array length
         *
         *  SC: O(S^2)
         *
         *  dp[i][j]: The number of ways to reach index i
         *            by taking j steps.
         *
         *  dp[i][j] = dp[i - 1][j - 1] + dp[i][j - 1] + dp[i + 1][j - 1]
         */

        vector<vector<long>> dp(s / 2 + 1, vector<long>(s + 1, -1));
        dp[0][0] = 1;
        return topDown(0, s, n, dp);
    }

private:
    long mod;

    long topDown(
            int i, int j, int n,
            vector<vector<long>>& dp) {

        if (i < 0 || i >= n || j < 0 || i > j) {
            return 0;
        }

        if (dp[i][j] != -1) {
            return dp[i][j];
        }

        long res = topDown(i - 1, j - 1, n, dp) +
                   topDown(i,     j - 1, n, dp) +
                   topDown(i + 1, j - 1, n, dp);
        return dp[i][j] = (res % mod);
    }
};
```