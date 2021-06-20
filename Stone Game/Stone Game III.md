
# Problem
### LeetCode 1406. Stone Game III
https://leetcode.com/problems/stone-game-iii

# Solution
```c++
class Solution {
public:
    string stoneGameIII(vector<int>& piles) {

        /**
         *  TC: O(N), where
         *      N is the number of stones
         * 
         *  SC: O(N)
         * 
         *  dp[i]: The optimal value difference that the current 
         *         player can acquire when considering the stones in
         *         the range [i, n)
         * 
         *  dp[i] = MAX | piles[i] - dp[i + 1]
         *              | piles[i] + piles[i + 1] - dp[i + 2]
         *              | piles[i] + piles[i + 1] + piles[i + 2] - dp[i + 3]
         */
        
        int n = piles.size();
        vector<int> dp(n, INT_MIN);
        
        int res = topDown(piles, 0, n, dp);
        if (res == 0) {
            return "Tie";
        }
        return res > 0 ? "Alice" : "Bob";
    }
    
private:
    int topDown(
            const vector<int>& piles,
            int i, int n,
            vector<int>& dp) {
        
        if (i == n) {
            return 0;
        }
        
        if (dp[i] != INT_MIN) {
            return dp[i];
        }
        
        int sum = piles[i];
        int opt = sum - topDown(piles, i + 1, n, dp);
        
        if (i + 1 < n) {
            sum += piles[i + 1];
            opt = max(opt, sum - topDown(piles, i + 2, n, dp));
        }
        
        if (i + 2 < n) {
            sum += piles[i + 2];
            opt = max(opt, sum - topDown(piles, i + 3, n, dp));
        }
        
        return dp[i] = opt;
    }
};
```