
# Problem
### LeetCode 773. Sliding Puzzle
https://leetcode.com/problems/sliding-puzzle

# Solution
```c++
struct Record {
    int x, y;
    string code;

    Record(int x, int y, const string& code)
        : x(x), y(y), code(code)
    { }
};


class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    int slidingPuzzle(vector<vector<int>>& board) {

        /**
         *  TC: O(N!), where
         *      N is the number of tiles
         *
         *  SC: O(N!)
         */

        auto zero = findZero(board);
        auto code = encode(board);

        if (code == "123450") {
            return 0;
        }

        queue<Record> q;
        q.emplace(zero.first, zero.second, code);

        unordered_set<string> visit;
        visit.emplace(move(code));

        int level = 0;

        while (!q.empty()) {
            int n = q.size();
            ++level;

            for (int i = 0 ; i < n ; ++i) {
                auto r = q.front();
                q.pop();

                int x = r.x;
                int y = r.y;
                auto& code = r.code;
                int src_offset = 3 * x + y;

                for (const auto& d : directs) {
                    int nx = x + d[0];
                    int ny = y + d[1];

                    if (!(nx >= 0 && ny >= 0 && nx < 2 && ny < 3)) {
                        continue;
                    }

                    int dst_offset = 3 * nx + ny;
                    swap(code[src_offset], code[dst_offset]);

                    if (visit.count(code) == 1) {
                        swap(code[src_offset], code[dst_offset]);
                        continue;
                    }

                    if (code == "123450") {
                        return level;
                    }

                    q.emplace(nx, ny, code);
                    visit.emplace(code);
                    swap(code[src_offset], code[dst_offset]);
                }
            }
        }

        return -1;
    }

private:
    vector<vector<int>> directs;

    string encode(const vector<vector<int>>& board) {
        string code(6, 0);
        code[0] = board[0][0] + '0';
        code[1] = board[0][1] + '0';
        code[2] = board[0][2] + '0';
        code[3] = board[1][0] + '0';
        code[4] = board[1][1] + '0';
        code[5] = board[1][2] + '0';
        return code;
    }

    pair<int, int> findZero(const vector<vector<int>>& board) {
        if (board[0][0] == 0) {
            return {0, 0};
        }
        if (board[0][1] == 0) {
            return {0, 1};
        }
        if (board[0][2] == 0) {
            return {0, 2};
        }
        if (board[1][0] == 0) {
            return {1, 0};
        }
        if (board[1][1] == 0) {
            return {1, 1};
        }
        if (board[1][2] == 0) {
            return {1, 2};
        }
        return {-1, -1};
    }
};
```