
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

        /**
         *  TC: O(2 ^ (M * N)), where
         *      M is the number of rows
         *      N is the number of columns
         *
         *  SC: O(2 ^ (M * N))
         */

        int m = mat.size();
        int n = mat[0].size();
        vector<bool> visit(1 << m * n);

        int code = encode(mat, m, n);
        if (code == 0) {
            return 0;
        }

        queue<int> q;
        q.emplace(code);

        int level = 0;

        while (!q.empty()) {
            int size = q.size();
            ++level;

            for (int i = 0 ; i < size ; ++i) {
                int src = q.front();
                q.pop();

                for (int x = 0 ; x < m ; ++x) {
                    for (int y = 0 ; y < n ; ++y) {
                        int dst = flip(src, m, n, x, y);

                        if (visit[dst]) {
                            continue;
                        }

                        if (dst == 0) {
                            return level;
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

    int flip(int code, int m, int n, int x, int y) {

        for (const auto& d : directs) {
            int nx = x + d[0];
            int ny = y + d[1];

            if (!(nx >= 0 && ny >= 0 && nx < m && ny < n)) {
                continue;
            }

            code ^= 1 << (nx * n + ny);
        }

        code ^= 1 << (x * n + y);
        return code;
    }

    int encode(const vector<vector<int>>& mat, int m, int n) {
        int code = 0;

        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                code |= mat[i][j] << (i * n + j);
            }
        }
        return code;
    }
};
```