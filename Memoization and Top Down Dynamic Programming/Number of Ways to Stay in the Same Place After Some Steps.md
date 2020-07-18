
# Problem
### LeetCode 1269. Number of Ways to Stay in the Same Place After Some Steps
https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps/

# Solution
```c++
class Solution {
public:
    int numWays(int steps, int arrLen) {

        /**
            dp[i][j]: The number of ways to reach offset j by taking i steps.

            dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j] + dp[i - 1][j + 1]
        */

        int n = min(arrLen, steps);
        vector<vector<long>> dp(steps + 1, vector<long>(n));
        dp[0][0] = 1;
        return topDown(dp, steps, 0, n) % MOD;
    }

private:
    static const int MOD = 1e9 + 7;

    long topDown(vector<vector<long>>& dp, int steps, int offset, int n) {

        if (steps < 0 || offset < 0 || offset >= n || offset > steps) {
            return 0;
        }

        if (dp[steps][offset] > 0) {
            return dp[steps][offset];
        }

        dp[steps][offset] =
            ((topDown(dp, steps - 1, offset + 1, n) % MOD) +
             (topDown(dp, steps - 1, offset, n) % MOD) +
             (topDown(dp, steps - 1, offset - 1, n) % MOD)) % MOD;
        return dp[steps][offset];
    }
};
```