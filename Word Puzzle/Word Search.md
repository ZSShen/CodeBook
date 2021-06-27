
# Problem
### LeetCode 79. Word Search
https://leetcode.com/problems/word-search

# Solution
```c++
class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    bool exist(vector<vector<char>>& board, string word) {

        /**
         *  TC: O(M * N * (3^L)), where
         *      M is the number of rows
         *      N is the number of columns
         *      L is the word length
         *
         *  SC: O(L)
         */

        int m = board.size();
        int n = board[0].size();
        int l = word.length();

        for (int x = 0 ; x < m ; ++x) {
            for (int y = 0 ; y < n ; ++y) {
                bool res = backTracking(x, y, m, n, 0, l, board, word);
                if (res) {
                    return true;
                }
            }
        }

        return false;
    }

private:
    vector<vector<int>> directs;

    bool backTracking(
            int x, int y, int m, int n,
            int i, int l,
            vector<vector<char>>& board,
            const string& word) {

        if (word[i] != board[x][y]) {
            return false;
        }

        ++i;
        if (i == l) {
            return true;
        }

        char backup = board[x][y];
        board[x][y] = 0;

        for (const auto& d : directs) {
            int nx = x + d[0];
            int ny = y + d[1];

            if (!(nx >= 0 && ny >= 0 && nx < m && ny < n) ||
                board[nx][ny] == 0) {
                continue;
            }

            bool res = backTracking(nx, ny, m, n, i, l, board, word);
            if (res) {
                return true;
            }
        }

        board[x][y] = backup;
        return false;
    }
};
```