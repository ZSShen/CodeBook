
# Problem
### LintCode 434. Number of Islands II
https://www.lintcode.com/problem/number-of-islands-ii/description

# Solution
```c++

class DisjointSet {
public:
    DisjointSet(int n)
        : count(0) {
    }

    void add(int x) {
        parent[x] = x;
        ++count;
    }

    int find(int x) {

        if (x == parent[x]) {
            return x;
        }

        return parent[x] = find(parent[x]);
    }

    void merge(int x, int y) {

        int px = find(x);
        int py = find(y);

        if (px == py) {
            return;
        }

        --count;
        parent[px] = py;
    }

    int query() {
        return count;
    }

private:
    int count;
    unordered_map<int, int> parent;
};


class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    vector<int> numIslands2(int m, int n, vector<vector<int>>& positions) {

        /**
         *  TC: O(K * log*(K)), where
         *      K is the number of given positions, or the potential number
         *      of islands
         *
         *  SC: O(M * N), where
         *      M is the number of rows
         *      N is the number of columns
         *
         *  00000       00000       01000        01000        01000
         *  00000  =>   01000   =>  01000   =>   01000   =>   01000
         *  00000       00000       00000        00000        00000
         *  00000       00000       00000        00010        00011
         *
         *           1 (1, 1)    2 (0, 1)     1 (1, 1)     1 (1, 1)
         *                       1 (1, 1)       (0, 1)       (0, 1)
         *
         *                       1 (1, 1)     3 (3, 3)     3 (3, 3)
         *                         (0, 1)                    (3, 4)
         */

        DisjointSet set(m * n);
        vector<vector<int>> grid(m, vector<int>(n));

        vector<int> ans;

        for (const auto& q : positions) {
            int x = q[0];
            int y = q[1];

            // If the grid cell is already part of an island,
            // we need to skip it to avoid duplicates
            if (grid[x][y] == 1) {
                ans.push_back(set.query());
                continue;
            }

            grid[x][y] = 1;
            int src_id = x * n + y;
            set.add(src_id);

            for (const auto& d : directs) {
                int nx = x + d[0];
                int ny = y + d[1];

                if (!(nx >= 0 && ny >= 0 && nx < m && ny < n) ||
                    grid[nx][ny] == 0) {
                    continue;
                }

                int dst_id = nx * n + ny;
                set.merge(src_id, dst_id);
            }

            ans.push_back(set.query());
        }

        return ans;
    }

private:
    vector<vector<int>> directs;
};
```