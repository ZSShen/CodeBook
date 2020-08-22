
# Problem
### LeetCode 403. Frog Jump
https://leetcode.com/problems/frog-jump

# Solution
```c++
class Solution {
public:
    bool canCross(vector<int>& stones) {
        /**
            state[i][j]: Determine if the frog can reach the destination,
            who is now standing at the ith position and is ready to take
            j units jump.
        */

        if (stones[0] != 0 || stones[1] != 1) {
            return false;
        }

        int n = stones.size();
        unordered_map<int, int> ref;
        for (int i = 0 ; i < n ; ++i) {
            ref[stones[i]] = i;
        }

        vector<unordered_map<int, bool>> memo(n);

        return topDown(ref, 1, n, memo, 1, 1);
    }

private:
    bool topDown(
            unordered_map<int, int>& stones,
            int i, int n,
            vector<unordered_map<int, bool>>& memo,
            int unit, int k) {

        // Reach the last stone.
        if (i == n - 1) {
            return true;
        }

        if (memo[i].count(k) == 1) {
            return memo[i][k];
        }

        // Try k - 1 unit.
        int next_unit = unit + k - 1;
        if (next_unit > unit && stones.count(next_unit) == 1) {
            int next_i = stones[next_unit];
            bool res = topDown(stones, next_i, n, memo, next_unit, k - 1);
            if (res) {
                return memo[i][k] = true;
            }
        }

        // Try k unit.
        next_unit = unit + k;
        if (next_unit > unit && stones.count(next_unit) == 1) {
            int next_i = stones[next_unit];
            bool res = topDown(stones, next_i, n, memo, next_unit, k);
            if (res) {
                return memo[i][k] = true;
            }
        }

        // Try k + 1 unit.
        next_unit = unit + k + 1;
        if (stones.count(next_unit) == 1) {
            int next_i = stones[next_unit];
            bool res = topDown(stones, next_i, n, memo, next_unit, k + 1);
            if (res) {
                return memo[i][k] = true;
            }
        }

        return memo[i][k] = false;
    }
};
```