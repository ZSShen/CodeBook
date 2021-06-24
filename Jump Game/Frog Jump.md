
# Problem
### LeetCode 403. Frog Jump
https://leetcode.com/problems/frog-jump

# Solution
```c++
class Solution {
public:
    bool canCross(vector<int>& stones) {

        /**
         *  TC: O(N^2), where
         *      N is the number of hops
         *
         *  SC: O(N^2)
         *
         * dp[i][j]: Whether we can reach the target if we take
         *           a j units jump to reach the ith hop
         */

        if (stones[0] != 0 || stones[1] != 1) {
            return false;
        }

        unordered_map<int, int> map;
        int n = stones.size();
        for (int i = 0 ; i < n ; ++i) {
            map[stones[i]] = i;
        }

        vector<unordered_map<int, bool>> memo(n);
        return topDown(map, 0, 0, n, 0, memo);
    }

private:
    bool topDown(
            unordered_map<int, int>& stones,
            int i, int num, int n, int k,
            vector<unordered_map<int, bool>>& memo) {

        if (i == n - 1) {
            return true;
        }

        if (memo[i].count(k) == 1) {
            return memo[i][k];
        }

        // Take k - 1 steps
        int next = num + k - 1;
        if (next > num && stones.count(next) == 1) {
            bool res = topDown(stones, stones[next], next, n, k - 1, memo);
            if (res) {
                return memo[i][k] = true;
            }
        }

        // Take k steps
        next = num + k;
        if (next > num && stones.count(next) == 1) {
            bool res = topDown(stones, stones[next], next, n, k, memo);
            if (res) {
                return memo[i][k] = true;
            }
        }

        // Take k + 1 steps
        next = num + k + 1;
        if (next > num && stones.count(next) == 1) {
            bool res = topDown(stones, stones[next], next, n, k + 1, memo);
            if (res) {
                return memo[i][k] = true;
            }
        }

        return memo[i][k] = false;
    }
};
```