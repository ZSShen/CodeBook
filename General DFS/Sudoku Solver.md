
# Problem
### LeetCode 37. Sudoku Solver
https://leetcode.com/problems/sudoku-solver

# Solution
```c++
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {

        /**
         *  TC: O(9 ^ (M * N)), where
         *      M is the number of rows
         *      N is the number of columns
         *
         *  SC: O(M * N)
         */

        vector<vector<bool>> rows(9, vector<bool>(10));
        vector<vector<bool>> cols(9, vector<bool>(10));
        vector<vector<bool>> mats(9, vector<bool>(10));

        for (int i = 0 ; i < 9 ; ++i) {
            for (int j = 0 ; j < 9 ; ++j) {
                if (board[i][j] == '.') {
                    continue;
                }
                int num = board[i][j] - '0';
                rows[i][num] = true;
                cols[j][num] = true;
                mats[getMatrixId(i, j)][num] = true;
            }
        }

        backTracking(board, 0, 0, 9, 9, rows, cols, mats);
    }

private:
    int getMatrixId(int x, int y) {
        return (x / 3) * 3 + y / 3;
    }

    bool backTracking(
            vector<vector<char>>& board,
            int x, int y, int m, int n,
            vector<vector<bool>>& rows,
            vector<vector<bool>>& cols,
            vector<vector<bool>>& mats) {

        if (x == m && y == 0) {
            return true;
        }

        int nx = x;
        int ny = y + 1;
        if (ny == n) {
            ny = 0;
            ++nx;
        }

        if (board[x][y] != '.') {
            return backTracking(board, nx, ny, m, n, rows, cols, mats);
        }

        for (int i = 1 ; i <= 9 ; ++i) {
            if (rows[x][i]) {
                continue;
            }
            if (cols[y][i]) {
                continue;
            }

            int mat_id = getMatrixId(x, y);
            if (mats[mat_id][i]) {
                continue;
            }

            board[x][y] = '0' + i;
            rows[x][i] = true;
            cols[y][i] = true;
            mats[mat_id][i] = true;

            bool res = backTracking(board, nx, ny, m, n, rows, cols, mats);
            if (res) {
                return true;
            }

            mats[mat_id][i] = false;
            cols[y][i] = false;
            rows[x][i] = false;
            board[x][y] = '.';
        }

        return false;
    }
};
```