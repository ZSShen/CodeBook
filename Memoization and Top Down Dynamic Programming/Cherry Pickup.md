
# Problem
### LeetCode 741. Cherry Pickup
https://leetcode.com/problems/cherry-pickup/

# Solution
```c++
class Solution {
public:
    int cherryPickup(vector<vector<int>>& grid) {

        int n = grid.size();

        vector<vector<vector<vector<int>>>>
            dp(n, vector<vector<vector<int>>>(
                n, vector<vector<int>>(
                    n, vector<int>(n, -1))));

        return max(0, topDown(grid, dp, n, 0, 0, 0, 0));
    }

private:
    int topDown(
            const vector<vector<int>>& grid,
            vector<vector<vector<vector<int>>>>& dp,
            int n, int r1, int c1, int r2, int c2) {

        if (!(r1 < n && c1 < n && r2 < n && c2 < n) ||
            grid[r1][c1] == -1 ||
            grid[r2][c2] == -1) {
            return INT_MIN;
        }

        if (dp[r1][c1][r2][c2] != -1) {
            return dp[r1][c1][r2][c2];
        }

        // The first person reaches the bottom right corner.
        if (r1 == n - 1 && c1 == n - 1) {
            return grid[n - 1][n - 1];
        }

        // The second person reaches the bottom right corner.
        if (r2 == n - 1 && c2 == n - 1) {
            return grid[n - 1][n - 1];
        }

        int cherry = 0;
        // If 2 people stand on the same place.
        if (r1 == r2 && c1 == c2) {
            cherry = grid[r1][c1];
        } else {
            cherry = grid[r1][c1] + grid[r2][c2];
        }

        int opt =
            max(
                max(topDown(grid, dp, n, r1 + 1, c1, r2 + 1, c2),
                    topDown(grid, dp, n, r1 + 1, c1, r2, c2 + 1)),
                max(topDown(grid, dp, n, r1, c1 + 1, r2 + 1, c2),
                    topDown(grid, dp, n, r1, c1 + 1, r2, c2 + 1))) + cherry;

        dp[r1][c1][r2][c2] = opt;
        return opt;
    }
};
```