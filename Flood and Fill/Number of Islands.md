
# Problem
### LeetCode 200. Number of Islands
https://leetcode.com/problems/number-of-islands

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int numIslands(vector<vector<char>>& grid) {

        /**
         *  TC: O(M * N), where
         *      M is the number of rows
         *      N is the number of columns
         *
         *  SC: O(M * N)
         */

        int m = grid.size();
        int n = grid[0].size();

        int ans = 0;

        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (grid[i][j] == '0') {
                    continue;
                }
                ++ans;
                dfs(grid, m, n, i, j);
            }
        }

        return ans;
    }

private:
    vector<vector<int>> directs;

    void dfs(
            vector<vector<char>>& grid,
            int m, int n, int x, int y) {

        grid[x][y] = '0';

        for (const auto& d : directs) {
            int nx = x + d[0];
            int ny = y + d[1];

            if (!(nx >= 0 && ny >= 0 && nx < m && ny < n) ||
                grid[nx][ny] == '0') {
                continue;
            }

            dfs(grid, m, n, nx, ny);
        }
    }
};
```