
# Problem
### LeetCode 1197. Minimum Knight Moves
https://leetcode.com/problems/minimum-knight-moves/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs(
            {{1, 2},
             {2, 1},
             {2, -1},
             {1, -2},
             {-1, -2},
             {-2, -1},
             {-2, 1},
             {-1, 2}})
    { }

    int minKnightMoves(int tx, int ty) {

        // For the boundary case.
        if (tx == 0 && ty == 0) {
            return 0;
        }

        tx = abs(tx);
        ty = abs(ty);

        unordered_set<int> visit;
        visit.emplace(0);

        queue<pair<int, int>> q;
        q.push({0, 0});

        int level = 0;
        while (!q.empty()) {
            int n = q.size();
            ++level;

            for (int i = 0 ; i < n ; ++i) {
                auto coord = q.front();
                q.pop();

                int x = coord.first;
                int y = coord.second;

                for (const auto& d : directs) {
                    int nx = x + d[0];
                    int ny = y + d[1];

                    int abs_nx = abs(nx);
                    int abs_ny = abs(ny);

                    int key = abs_nx * dim + abs_ny;
                    if (visit.count(key) == 1) {
                        continue;
                    }

                    // Check for the target.
                    if (abs_nx == tx && abs_ny == ty) {
                        return level;
                    }

                    visit.emplace(key);
                    q.push({nx, ny});
                }
            }
        }

        // Should not reach here.
        return -1;
    }

private:
    static const int dim = 1e4;

    vector<vector<int>> directs;
};
```