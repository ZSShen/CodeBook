
# Problem
### LeetCode 317. Shortest Distance from All Buildings
https://leetcode.com/problems/shortest-distance-from-all-buildings

# Solution
```c++
class Solution {
public:
    Solution() {
        directs.push_back({1, 0});
        directs.push_back({-1, 0});
        directs.push_back({0, 1});
        directs.push_back({0, -1});
    }

    int shortestDistance(vector<vector<int>>& grid) {

        /**
         *  TC: O(B * M * N), where
         *      B is the number of buildings
         *      M is the number of grid rows
         *      N is the number of grid columns
         *
         *  SC: O(M * N)
         */

        int m = grid.size();
        int n = grid[0].size();

        vector<vector<int>> dist(m, vector<int>(n));
        vector<vector<int>> hit(m, vector<int>(n));
        vector<pair<int, int>> buildings;

        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (grid[i][j] == 1) {
                    buildings.push_back({i, j});
                }
            }
        }

        for (const auto& building : buildings) {
            helper(building.first, building.second,
                   m, n, grid, dist, hit);
        }

        int ans = INT_MAX;

        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (hit[i][j] == buildings.size()) {
                    ans = min(ans, dist[i][j]);
                }
            }
        }

        return ans < INT_MAX ? ans : -1;
    }

private:
    vector<vector<int>> directs;

    void helper(
            int sr, int sc, int m, int n,
            const vector<vector<int>>& grid,
            vector<vector<int>>& dist,
            vector<vector<int>>& hit) {

        queue<pair<int, int>> q;
        q.push({sr, sc});

        vector<vector<bool>> visit(m, vector<bool>(n));
        visit[sr][sc] = true;

        int level = 0;

        while (!q.empty()) {
            int size = q.size();
            ++level;

            for (int i = 0 ; i < size ; ++i) {
                auto rec = q.front();
                q.pop();

                for (const auto& d : directs) {
                    int nr = rec.first + d[0];
                    int nc = rec.second + d[1];

                    if (!(nr >= 0 && nc >= 0 && nr < m && nc < n) ||
                        visit[nr][nc] ||
                        grid[nr][nc] != 0) {
                        continue;
                    }

                    dist[nr][nc] += level;
                    ++hit[nr][nc];
                    visit[nr][nc] = true;
                    q.push({nr, nc});
                }
            }
        }
    }
};
```
