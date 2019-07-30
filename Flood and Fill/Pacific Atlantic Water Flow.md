
# Problem
### LintCode 778. Pacific Atlantic Water Flow
https://www.lintcode.com/problem/pacific-atlantic-water-flow/description

# Solution
```c++

struct Record {
    int x;
    int y;

    Record(int x, int y)
      : x(x), y(y)
    { }
};


class Solution {
public:
    Solution()
      : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    /**
     * @param matrix: the given matrix
     * @return: The list of grid coordinates
     */
    vector<vector<int>> pacificAtlantic(vector<vector<int>> &matrix) {
        // write your code here

        int num_r = matrix.size();
        if (num_r == 0) {
            return {};
        }

        int num_c = matrix[0].size();
        if (num_c == 0) {
            return {};
        }

        std::vector<std::vector<char>> kinds(num_r, std::vector<char>(num_c, 0));

        for (int i = 0 ; i < num_c ; ++i) {
            floodAndFill(kinds, matrix, 0, i, num_r, num_c, Ocean::P);
        }
        for (int i = 1 ; i < num_r ; ++i) {
            floodAndFill(kinds, matrix, i, 0, num_r, num_c, Ocean::P);
        }

        for (int i = 0 ; i < num_r ; ++i) {
            floodAndFill(kinds, matrix, i, num_c - 1, num_r, num_c, Ocean::A);
        }
        for (int i = 0 ; i < num_c - 1 ; ++i) {
            floodAndFill(kinds, matrix, num_r - 1, i, num_r, num_c, Ocean::A);
        }

        std::vector<std::vector<int>> ans;
        for (int i = 0 ; i < num_r ; ++i) {
            for (int j = 0 ; j < num_c ; ++j) {
                if (kinds[i][j] == Ocean::Combine) {
                    ans.push_back({i, j});
                }
            }
        }

        return ans;
    }

private:
    void floodAndFill(
        auto& kinds, const auto& matrix,
        int r, int c, int num_r, int num_c, char kind) {

        std::vector<std::vector<bool>>
            visit(num_r, std::vector<bool>(num_c, false));
        visit[r][c] = true;

        std::queue<Record> queue;
        queue.push(Record(r, c));

        while (!queue.empty()) {
            auto rec = queue.front();
            queue.pop();

            int x = rec.x;
            int y = rec.y;

            // Set the ocean flag.
            kinds[x][y] = kinds[x][y] | kind;

            for (const auto& direct : directs) {
                int nx = x + direct[0];
                int ny = y + direct[1];

                if (!(nx >= 0 && ny >= 0 && nx < num_r && ny < num_c) ||
                    visit[nx][ny] ||
                    matrix[nx][ny] < matrix[x][y]) {
                    continue;
                }

                visit[nx][ny] = true;
                queue.push(Record(nx, ny));
            }
        }
    }

    enum Ocean {
        P = 1,
        A = 2,
        Combine = 3
    };

    std::vector<std::vector<int>> directs;
};
```