
# Problem
### LintCode 778. Pacific Atlantic Water Flow
https://www.lintcode.com/problem/pacific-atlantic-water-flow/description

# Solution
```c++
class Solution {
public:
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& matrix) {

        int m = matrix.size();
        if (m == 0) {
            return {};
        }
        int n = matrix[0].size();
        if (n == 0) {
            return {};
        }

        vector<vector<bool>> pacific(m, vector<bool>(n, false));
        vector<vector<bool>> atlantic(m, vector<bool>(n, false));

        for (int i = 0 ; i < m ; ++i) {
            floodAndFill(matrix, pacific, m, n, i, 0, 0);
            floodAndFill(matrix, atlantic, m, n, i, n - 1, 0);
        }
        for (int i = 0 ; i < n ; ++i) {
            floodAndFill(matrix, pacific, m, n, 0, i, 0);
            floodAndFill(matrix, atlantic, m, n, m - 1, i, 0);
        }

        vector<vector<int>> ans;
        for (int i = 0 ; i < m ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (pacific[i][j] && atlantic[i][j]) {
                    ans.push_back({i, j});
                }
            }
        }

        return ans;
    }

private:
    void floodAndFill(
        const auto& board, auto& ocean,
        int m, int n, int r, int c,
        int h) {

        if (r < 0 || c < 0 || r >= m || c >= n) {
            return;
        }
        if (board[r][c] < h) {
            return;
        }
        if (ocean[r][c]) {
            return;
        }

        ocean[r][c] = true;

        floodAndFill(board, ocean, m, n, r - 1, c, board[r][c]);
        floodAndFill(board, ocean, m, n, r + 1, c, board[r][c]);
        floodAndFill(board, ocean, m, n, r, c - 1, board[r][c]);
        floodAndFill(board, ocean, m, n, r, c + 1, board[r][c]);
    }
};
```