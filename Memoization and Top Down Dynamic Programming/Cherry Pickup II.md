
# Problem
### LeetCode 1463. Cherry Pickup II
https://leetcode.com/problems/cherry-pickup-ii/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({
            {-1, -1}, {-1, 0}, {-1, 1},
            {0,  -1}, { 0, 0}, { 0, 1},
            {1,  -1}, { 1, 0}, { 1, 1}})
        { }

    int cherryPickup(vector<vector<int>>& grid) {

        /**
            (i, j)
            -> (i, j - 1)
            -> (i, j)
            -> (i, j + 1)

            (i, k)
            -> (i, k - 1)
            -> (i, k)
            -> (i, k + 1)


            dp[i][j][k] = MAX{
                        func(i + 1, j - 1, k - 1),
                        func(i + 1, j - 1, k),
                        func(i = 1, j - 1, k + 1),
                        ... }
        */

        int m = grid.size();
        int n = grid[0].size();

        vector<vector<vector<int>>>
            dp(m, vector<vector<int>>(n, vector<int>(n, 0)));

        return topDown(grid, m, n, dp, 0, 0, n - 1);
    }

private:
    vector<vector<int>> directs;

    int topDown(
            vector<vector<int>>& grid,
            int m, int n,
            vector<vector<vector<int>>>& dp,
            int i, int j, int k) {

        if (i == m) {
            return 0;
        }

        if (dp[i][j][k] != 0) {
            return dp[i][j][k];
        }

        int opt;
        if (j == k) {
            opt = grid[i][j];
        } else {
            opt = grid[i][j] + grid[i][k];
        }

        int res = 0;
        for (const auto& direct : directs) {
            int nj = j + direct[0];
            int nk = k + direct[1];

            if (!(nj >= 0 && nk >= 0 && nj < n && nk < n)) {
                continue;
            }

            res = max(res, topDown(grid, m, n, dp, i + 1, nj, nk));
        }

        dp[i][j][k] = opt + res;
        return dp[i][j][k];
    }
};
```