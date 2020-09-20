
# Problem
### LeetCode 980. Unique Paths III
https://leetcode.com/problems/unique-paths-iii/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}}), base(20)
    { }

    int uniquePathsIII(vector<vector<int>>& grid) {

        int m = grid.size();
        int n = grid[0].size();

        int k = 0;
        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (grid[i][j] == 0) {
                    ++k;
                }
            }
        }

        int ans = 0;
        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (grid[i][j] == 1) {
                    dfs(grid, i, j, m, n, 0, k, ans);
                    break;
                }
            }
        }

        return ans;
    }

private:
    vector<vector<int>> directs;
    int base;

    void dfs(
            vector<vector<int>>& grid,
            int r, int c, int m, int n,
            int pc, int k, int& ans) {

        if (grid[r][c] == 2 && pc == k) {
            ++ans;
            return;
        }

        int backup = grid[r][c];
        grid[r][c] = -1;

        for (const auto& d : directs) {
            int nr = r + d[0];
            int nc = c + d[1];

            if (!(nr >= 0 && nc >= 0 && nr < m && nc < n) ||
                grid[nr][nc] == -1) {
                continue;
            }

            if (grid[nr][nc] == 0) {
                ++pc;
            }

            dfs(grid, nr, nc, m, n, pc, k, ans);

            if (grid[nr][nc] == 0) {
                --pc;
            }
        }

        grid[r][c] = backup;
    }
};
```