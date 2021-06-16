
# Problem
### LeetCode 51. N-Queens
https://leetcode.com/problems/n-queens

# Solution
```c++
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {

        /**
         *  TC: O(N!), where
         *      N is the board size
         *
         *  SC: O(N)
         */

        vector<vector<string>> ans;
        vector<int> queens;
        backTracking(0, n, queens, ans);
        return ans;
    }

private:
    void backTracking(
            int c, int n,
            vector<int>& queens,
            vector<vector<string>>& ans) {

        if (c == n) {
            vector<string> config(n, string(n, '.'));
            for (int c = 0 ; c < n ; ++c) {
                int r = queens[c];
                config[r][c] = 'Q';
            }
             ans.emplace_back(move(config));
            return;
        }

        for (int r = 0 ; r < n ; ++r) {
            int size = queens.size();
            bool conflict = false;

            for (int y = 0 ; y < size ; ++y) {
                int x = queens[y];

                // Ensure no row conflict.
                if (x == r) {
                    conflict = true;
                    break;
                }

                // Ensure no diagonal conflict.
                if (x - y == r - c) {
                    conflict = true;
                    break;
                }

                // Ensure no anti-diagonal conflict.
                if (x + y == r + c) {
                    conflict = true;
                    break;
                }
            }

            if (conflict) {
                continue;
            }

            queens.emplace_back(r);
            backTracking(c + 1, n, queens, ans);
            queens.pop_back();
        }
    }
};
```