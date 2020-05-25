
# Problem
### LintCode 877. Stone Game
https://leetcode.com/problems/stone-game/

# Solution
```c++
class Solution {
public:
    bool stoneGame(vector<int>& piles) {

        /**
            piles[i] -> piles[j]

            select(piles, i, j):
                The maximum score difference Alex can get from
                the piles starting at index i and ending at index j.

            MAX(piles[i] - select(piles, i + 1, j),
                piles[j] - select(piles, i, j - 1))


            dp[i][j]: Just like the objective function

            dp[i][j] = MAX | piles[i] - dp[i + 1][j]
                           | piles[j] - dp[i][j - 1]
        */

        int n = piles.size();

        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int i = 0 ; i < n ; ++i) {
            dp[i][i] = piles[i];
        }

        for (int l = 2 ; l <= n ; ++l) {
            for (int i = 0, j = i + l - 1 ; i <= n - l ; ++i, ++j) {
                dp[i][j] = max(piles[i] - dp[i + 1][j],
                               piles[j] - dp[i][j - 1]);
            }
        }

        return dp[0][n - 1] > 0;
    }
};
```