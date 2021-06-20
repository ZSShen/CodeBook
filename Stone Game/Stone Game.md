
# Problem
### LeetCode 877. Stone Game
https://leetcode.com/problems/stone-game

# Solution
```c++
class Solution {
public:
    bool stoneGame(vector<int>& piles) {

        /**
         *  TC: O(N^2), where
         *      N is the number of stons
         *  
         *  SC: O(N^2)
         * 
         *  dp[i][j]: The optimal value difference that the current 
         *            player can acquire when considering stones in the 
         *            range (i, j).
         * 
         *  dp[i][j] = MAX | piles[i] - dp[i + 1][j]
         *                 | piles[j] - dp[i][j - 1]
         */

        int n = piles.size();
        vector<vector<int>> dp(n, vector<int>(n, INT_MIN));
        return topDown(piles, 0, n - 1, dp) > 0;
    }
    
private:
    int topDown(
            const vector<int>& piles,
            int i, int j,
            vector<vector<int>>& dp) {
        
        if (i == j) {
            return piles[i];
        }
        
        if (dp[i][j] != INT_MIN) {
            return dp[i][j];
        }
        
        int opt = max(
                piles[i] - topDown(piles, i + 1, j, dp),
                piles[j] - topDown(piles, i , j - 1, dp)
            );
        return dp[i][j] = opt;
    }
};
```