
# Problem
### LeetCode 1263. Minimum Moves to Move a Box to Their Target Location
https://leetcode.com/problems/minimum-moves-to-move-a-box-to-their-target-location

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int minPushBox(vector<vector<char>>& grid) {

        /**
         *  TC: O((R^2) * (C^2)), where
         *      R is the number of rows
         *      C is the number of columns
         *
         *  SC: O(R*C)
         */

        int m = grid.size();
        int n = grid[0].size();

        int player, box, target;

        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                switch (grid[i][j]) {
                    case 'S':
                        player = i * n + j;
                        break;
                    case 'B':
                        box = i * n + j;
                        break;
                    case 'T':
                        target = i * n + j;
                        break;
                }
            }
        }

        unordered_set<string> visit;

        // (box, player)
        queue<pair<int, int>> q;
        q.push({box, player});

        int level = 0;

        while (!q.empty()) {
            int size = q.size();
            ++level;

            for (int i = 0 ; i < size ; ++i) {
                auto r = q.front();
                q.pop();

                box = r.first;
                player = r.second;

                int box_x = box / n, box_y = box % n;

                for (const auto& d : directs) {

                    int nx = box_x + d[0];
                    int ny = box_y + d[1];
                    if (!(nx >= 0 && ny >= 0 && nx < m && ny < n) ||
                        grid[nx][ny] == '#') {
                        continue;
                    }

                    int next_box = nx * n + ny;

                    int px = box_x - d[0];
                    int py = box_y - d[1];
                    if (!(px >= 0 && py >= 0 && px < m && py < n) ||
                        grid[px][py] == '#') {
                        continue;
                    }

                    int move = px * n + py;

                    string id = to_string(next_box) + "," + to_string(move);
                    if (visit.count(id) == 1) {
                        continue;
                    }

                    // Check if the player is able to stand behind the box.
                    if (!canReach(m, n, grid, player, move, box)) {
                        continue;
                    }

                    if (next_box == target) {
                        return level;
                    }

                    visit.emplace(id);
                    q.push({next_box, box});
                }
            }
        }

        return -1;
    }

private:
    vector<vector<int>> directs;

    bool canReach(
            int m, int n,
            const vector<vector<char>>& grid,
            int start, int target, int box) {

        unordered_set<int> visit;
        visit.emplace(box);

        queue<int> q;
        q.emplace(start);

        while (!q.empty()) {
            auto r = q.front();
            q.pop();

            int x = r / n, y = r % n;

            for (const auto& d : directs) {
                int nx = x + d[0];
                int ny = y + d[1];

                if (!(nx >= 0 && ny >= 0 && nx < m && ny < n) ||
                    grid[nx][ny] == '#') {
                    continue;
                }

                int next = nx * n + ny;
                if (visit.count(next) == 1) {
                    continue;
                }

                if (next == target) {
                    return true;
                }

                visit.emplace(next);
                q.push(next);
            }
        }

        return false;
    }

};
```