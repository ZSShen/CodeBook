
# Problem
### LeetCode 1284. Minimum Number of Flips to Convert Binary Matrix to Zero Matrix
https://leetcode.com/problems/minimum-number-of-flips-to-convert-binary-matrix-to-zero-matrix/

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int minFlips(vector<vector<int>>& mat) {

        int m = mat.size();
        int n = mat[0].size();

        int root = encode(mat, m, n);
        if (root == 0) {
            return 0;
        }

        queue<int> q;
        q.emplace(root);

        int step = 0;
        vector<bool> visit(1 << (m * n), false);
        visit[root] = true;

        while (!q.empty()) {
            int size = q.size();
            ++step;

            for (int i = 0 ; i < size ; ++i) {
                int src = q.front();
                q.pop();

                for (int x = 0 ; x < m ; ++x) {
                    for (int y = 0 ; y < n ; ++y) {
                        int dst = flip(x, y, m, n, src);

                        if (visit[dst]) {
                            continue;
                        }

                        if (dst == 0) {
                            return step;
                        }

                        visit[dst] = true;
                        q.emplace(dst);
                    }
                }
            }
        }

        return -1;
    }

private:
    vector<vector<int>> directs;

    int getIndex(int x, int y, int n) {
        return x * n + y;
    }

    int flip(int x, int y, int m, int n, int src) {
        int dst = src;

        for (const auto& direct : directs) {
            int nx = x + direct[0];
            int ny = y + direct[1];

            if (!(nx >= 0 && ny >= 0 && nx < m && ny < n)) {
                continue;
            }

            dst ^= (1 << getIndex(nx, ny, n));
        }

        dst ^= (1 << getIndex(x, y, n));
        return dst;
    }

    int encode(vector<vector<int>>& mat, int m, int n) {
        int enc = 0;

        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (mat[i][j] == 1) {
                    enc ^= (1 << getIndex(i, j, n));
                }
            }
        }

        return enc;
    }
};
```