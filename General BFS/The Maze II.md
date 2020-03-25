
# Problem
### LeetCode 505. The Maze II
https://leetcode.com/problems/the-maze-ii/

# Solution
```c++

struct Record {
    int x;
    int y;
    int dist;

    Record(int x, int y, int dist)
        : x(x), y(y), dist(dist)
    { }
};


class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int shortestDistance(vector<vector<int>>& maze, vector<int>& start, vector<int>& end) {

        int m = maze.size();
        if (m == 0) {
            return 0;
        }

        int n = maze[0].size();
        if (n == 0) {
            return 0;
        }

        queue<Record> queue;
        queue.emplace(start[0], start[1], 0);

        vector<vector<int>> dp(m, vector<int>(n, INT_MAX));
        dp[start[0]][start[1]] = 0;

        while (!queue.empty()) {
            int size = queue.size();

            for (int i = 0 ; i < size ; ++i) {
                auto record = queue.front();
                queue.pop();

                int x = record.x;
                int y = record.y;
                int dist = record.dist;

                for (const auto& direct : directs) {
                    int nx = x + direct[0];
                    int ny = y + direct[1];
                    int new_dist = dist;

                    while ((nx >= 0 && ny >= 0 && nx < m && ny < n) &&
                            maze[nx][ny] == 0) {
                        nx += direct[0];
                        ny += direct[1];
                        ++new_dist;
                    }

                    nx -= direct[0];
                    ny -= direct[1];

                    if (new_dist < dp[nx][ny]) {
                        dp[nx][ny] = new_dist;
                        if (nx != end[0] || ny != end[1]) {
                            queue.emplace(nx, ny, new_dist);
                        }

                    }
                }
            }
        }

        return dp[end[0]][end[1]] == INT_MAX ? -1 : dp[end[0]][end[1]];
    }

private:
    vector<vector<int>> directs;
};
```