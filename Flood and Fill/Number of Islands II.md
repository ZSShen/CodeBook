
# Problem
### LintCode 434. Number of Islands II
https://www.lintcode.com/problem/number-of-islands-ii/description

# Solution
```c++
class DisjointSet {
public:
    DisjointSet()
      : count(0)
    { }

    void add(int x) {
        parent[x] = x;
        ++count;
    }

    int find(int x) {

        if (parent[x] == x) {
            return x;
        }

        parent[x] = find(parent[x]);
        return parent[x];
    }

    void unite(int x, int y) {

        int px = find(x);
        int py = find(y);

        if (px != py) {
            parent[px] = py;
            --count;
        }
    }

    int getNumberOfSets() {
        return count;
    }

private:
    int count;
    std::unordered_map<int, int> parent;
};


class Solution {
public:
    Solution()
      : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    /**
     * @param n: An integer
     * @param m: An integer
     * @param operators: an array of point
     * @return: an integer array
     */
    vector<int> numIslands2(int n, int m, vector<Point> &operators) {
        // write your code here

        /**
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

        std::vector<int> ans;
        std::vector<std::vector<int>> grid(n, std::vector<int>(m, 0));
        DisjointSet set;

        for (const auto& op : operators) {
            int x = op.x;
            int y = op.y;

            // Should avoid the dpulicated operations.
            if (grid[x][y] != 0) {
                ans.push_back(set.getNumberOfSets());
                continue;
            }

            int id = generateId(m, x, y);
            set.add(id);
            grid[x][y] = id;

            for (const auto& direct : directs) {
                int nx = x + direct[0];
                int ny = y + direct[1];

                if (!(nx >=0 && ny >= 0 && nx < n && ny < m) ||
                    grid[nx][ny] == 0) {
                    continue;
                }

                set.unite(id, grid[nx][ny]);
            }

            ans.push_back(set.getNumberOfSets());
        }

        return ans;
    }

private:
    int generateId(int m, int x, int y) {
        return m * x + y + 1;
    }

    std::vector<std::vector<int>> directs;
};
```