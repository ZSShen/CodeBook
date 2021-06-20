
# Problem
### LeetCode 494. Target Sum
https://leetcode.com/problems/target-sum

# Solution
```c++
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {

        /**
         *  TC: O(N * T), where
         *      N is the number of elements
         *      T is the target sum
         *
         *  SC: O(N * T)
         */

        int n = nums.size();
        vector<unordered_map<int, int>> memo(n);
        return topDown(nums, 0, n, target, memo);
    }

private:
    int topDown(
            const vector<int>& nums,
            int i, int n, long sum,
            vector<unordered_map<int, int>>& memo) {

        if (i == n) {
            return sum == 0;
        }

        if (memo[i].count(sum) == 1) {
            return memo[i][sum];
        }

        int res = topDown(nums, i + 1, n, sum - nums[i], memo) +
                  topDown(nums, i + 1, n, sum + nums[i], memo);
        return memo[i][sum] = res;
    }
};
```