
# Problem
### LeetCode 827. Making A Large Island
https://leetcode.com/problems/making-a-large-island/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int largestIsland(vector<vector<int>>& grid) {

        int color = 2;
        unordered_map<int, int> areas;

        int ans = 0;

        int n = grid.size();
        for (int x = 0 ; x < n ; ++x) {
            for (int y = 0 ; y < n ; ++y) {
                if (grid[x][y] != 1) {
                    continue;
                }
                areas[color] = runDFS(n, x, y, grid, color);
                ans = max(ans, areas[color]);
                ++color;
            }
        }

        for (int x = 0 ; x < n ; ++x) {
            for (int y = 0 ; y < n ; ++y) {
                if (grid[x][y] != 0) {
                    continue;
                }

                unordered_set<int> select;
                int area = 1;

                for (const auto& d : directs) {
                    int nx = x + d[0];
                    int ny = y + d[1];

                    if (!(nx >= 0 && ny >= 0 && nx < n && ny < n) ||
                        grid[nx][ny] < 2 ||
                        select.count(grid[nx][ny]) == 1) {
                        continue;
                    }

                    area += areas[grid[nx][ny]];
                    select.emplace(grid[nx][ny]);
                }

                ans = max(ans, area);
            }
        }

        return ans;
    }

private:
    vector<vector<int>> directs;

    int runDFS(
            int n, int x, int y,
            vector<vector<int>>& grid,
            int color) {

        int area = 1;
        grid[x][y] = color;

        for (const auto& d : directs) {
            int nx = x + d[0];
            int ny = y + d[1];

            if (!(nx >= 0 && ny >= 0 && nx < n && ny < n) ||
                grid[nx][ny] != 1) {
                continue;
            }

            area += runDFS(n, nx, ny, grid, color);
        }

        return area;
    }
};
```