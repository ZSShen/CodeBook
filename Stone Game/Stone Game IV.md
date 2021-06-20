
# Problem
### LeetCode 1510. Stone Game IV
https://leetcode.com/problems/stone-game-iv

# Solution
```c++
class Solution {
public:
    bool winnerSquareGame(int n) {

        /**
         *  TC: O(N * sqrt(N)), where
         *      N is the number of stones
         * 
         *  SC: O(N)
         * 
         *  dp[i]: Whether the current player can win the game
         *         when there are i stones remained
         * 
         *  dp[i] = OR{ dp[i - j * j] | i >= j * j }
         */
        
        vector<char> dp(n, -1);
        return topDown(0, n, dp);
    }
    
private:
    bool topDown(
        int i, int n, vector<char>& dp) {
        
        if (i == n) {
            return false;
        }
        
        if (dp[i] != -1) {
            return dp[i];
        }
        
        bool res = false;
        for (int j = 1 ; i + j * j <= n ; ++j) {
            res = res || !topDown(i + j * j, n, dp);
            if (res) {
                break;
            }
        }
        return dp[i] = res;
    }
};
```