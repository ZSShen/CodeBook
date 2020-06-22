
# Problem
### LeetCode 1293. Shortest Path in a Grid with Obstacles Elimination
https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int shortestPath(vector<vector<int>>& grid, int k) {

        int m = grid.size();
        int n = grid[0].size();

        vector<vector<int>> dp(m, vector<int>(n, INT_MAX));

        queue<tuple<int, int, int>> q;
        q.emplace(0, 0, 0);

        int step = 0;

        while (!q.empty()) {
            int size = q.size();

            for (int i = 0 ; i < size ; ++i) {
                int x, y, o;

                tie(x, y, o) = q.front();
                q.pop();

                if (x == m - 1 && y == n - 1) {
                    return step;
                }

                for (const auto& direct : directs) {
                    int nx = x + direct[0];
                    int ny = y + direct[1];

                    if (!(nx >= 0 && ny >= 0 && nx < m && ny < n)) {
                        continue;
                    }

                    int no = o + grid[nx][ny];
                    if (no > k || no >= dp[nx][ny]) {
                        continue;
                    }

                    dp[nx][ny] = no;
                    q.emplace(nx, ny, no);
                }
            }

            ++step;
        }

        return -1;
    }

private:
    vector<vector<int>> directs;
};
```