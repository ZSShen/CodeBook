
# Problem
### LeetCode 286. Walls and Gates
https://leetcode.com/problems/walls-and-gates/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    void wallsAndGates(vector<vector<int>>& rooms) {

        int m = rooms.size();
        if (m == 0) {
            return;
        }

        int n = rooms[0].size();
        if (n == 0) {
            return;
        }

        queue<pair<int, int>> queue;
        for (int r = 0 ; r < m ; ++r) {
            for (int c = 0 ; c < n ; ++c) {
                if (rooms[r][c] == 0) {
                    queue.emplace(r, c);
                }
            }
        }

        int dist = 0;
        while (!queue.empty()) {
            ++dist;
            int size = queue.size();

            for (int i = 0 ; i < size ; ++i) {
                auto rec = queue.front();
                queue.pop();

                int r = rec.first;
                int c = rec.second;

                for (const auto& direct : directs) {
                    int nr = r + direct[0];
                    int nc = c + direct[1];

                    if (!(nr >= 0 && nc >= 0 && nr < m && nc < n) ||
                       rooms[nr][nc] != INF ||
                       rooms[nr][nc] == -1 ||
                       rooms[nr][nc] == 0) {
                        continue;
                    }

                    rooms[nr][nc] = min(rooms[nr][nc], dist);
                    queue.emplace(nr, nc);
                }
            }
        }
    }

private:
    vector<vector<int>> directs;

    static const int INF = 2147483647;
};
```