
# Problem
### LeetCode 329. Longest Increasing Path in a Matrix
https://leetcode.com/problems/longest-increasing-path-in-a-matrix/

# Solution
```c++
class Solution {
public:
    int longestIncreasingPath(vector<vector<int>>& matrix) {

        int m = matrix.size();
        if (m == 0) {
            return 0;
        }

        int n = matrix[0].size();
        if (n == 0) {
            return 0;
        }

        vector<vector<int>> dp(m, vector<int>(n));
        int lis = INT_MIN;

        for (int r = 0 ; r < m ; ++r) {
            for (int c = 0 ; c < n ; ++c) {
                lis = max(lis, topDown(m, n, r, c, matrix, dp, -1));
            }
        }

        return lis;
    }

private:
    int topDown(
            int m, int n, int r, int c,
            vector<vector<int>>& matrix,
            vector<vector<int>>& dp,
            int pred) {

        if (r < 0 || r == m || c < 0 || c == n || pred >= matrix[r][c]) {
            return 0;
        }

        if (dp[r][c] > 0) {
            return dp[r][c];
        }

        int lis = 1;
        lis = max(lis, 1 + topDown(m, n, r - 1, c, matrix, dp, matrix[r][c]));
        lis = max(lis, 1 + topDown(m, n, r + 1, c, matrix, dp, matrix[r][c]));
        lis = max(lis, 1 + topDown(m, n, r, c - 1, matrix, dp, matrix[r][c]));
        lis = max(lis, 1 + topDown(m, n, r, c + 1, matrix, dp, matrix[r][c]));

        dp[r][c] = lis;
        return lis;
    }
};
```