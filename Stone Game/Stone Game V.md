
# Problem
### LeetCode 1563. Stone Game V
https://leetcode.com/problems/stone-game-v

# Solution
```c++
class Solution {
public:
    int stoneGameV(vector<int>& piles) {

        /**
         *  TC: O(N ^ 3), where
         *      N is the number of stones
         *
         *  SC: O(N ^ 2)
         */

        int n = piles.size();
        vector<int> prefix(n + 1);
        for (int i = 0 ; i < n ; ++i) {
            prefix[i + 1] = prefix[i] + piles[i];
        }

        vector<vector<int>> dp(n, vector<int>(n, -1));
        return topDown(prefix, 0, n - 1, dp);
    }

private:
    int topDown(
            const vector<int>& prefix,
            int i, int j,
            vector<vector<int>>& dp) {

        if (i == j) {
            return 0;
        }
        if (dp[i][j] != -1) {
            return dp[i][j];
        }

        int opt = INT_MIN;

        for (int k = i ; k < j ; ++k) {
            int left = prefix[k + 1] - prefix[i];
            int right = prefix[j + 1] - prefix[k + 1];

            if (left > right) {
                opt = max(opt, right + topDown(prefix, k + 1, j, dp));
                continue;
            }
            if (right > left) {
                opt = max(opt, left + topDown(prefix, i, k, dp));
                continue;
            }

            opt = max(opt, right + topDown(prefix, k + 1, j, dp));
            opt = max(opt, left + topDown(prefix, i, k, dp));
        }

        return dp[i][j] = opt;
    }
};
```