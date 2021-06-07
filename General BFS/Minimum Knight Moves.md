
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

        /**
         *  TC: O(|X| * |Y|), where
         *      |X| is the x index in the first quadrant
         *      |Y| is the y index in the first quadrant
         *
         *  SC: O(|X| * |Y|)
         */

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
            int size = q.size();
            ++level;

            for (int i = 0 ; i < size ; ++i) {
                auto p = q.front();
                q.pop();
                int x = p.first;
                int y = p.second;

                for (const auto& d : directs) {
                    int nx = x + d[0];
                    int ny = y + d[1];
                    int np = nx * dim + ny;

                    // We set this boundary to cover the target point like (1, 1).
                    // In such case, we can visit (2, -1) and then go to (1, 1),
                    // resulting in 2 steps.
                    // However, if we set boundary to x = 0 and y = 0, the possible
                    // shortest path will become (0, 0), (2, 1), (0, 2), (2, 3), and (1, 1),
                    // resulting in 4 steps, which is suboptimal.
                    if (!(nx >= -1 && ny >= -1) || visit.count(np) == 1) {
                        continue;
                    }

                    if (nx == tx && ny == ty) {
                        return level;
                    }

                    q.push({nx, ny});
                    visit.emplace(np);
                }
            }
        }

        // Should never reach here.
        return -1;
    }

private:
    static const int dim = 1e4;

    vector<vector<int>> directs;
};
```