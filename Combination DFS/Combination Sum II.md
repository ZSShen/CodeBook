
# Problem
### LeetCode 40. Combination Sum II
https://leetcode.com/problems/combination-sum-ii

# Solution
```c++
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& nums, int target) {

        /**
         *  TC: O(N * 2^N), where
         *      N is the number elements
         *
         *  SC: O(N)
         */

        sort(nums.begin(), nums.end());

        vector<int> conf;
        vector<vector<int>> ans;

        backTracking(nums, 0, nums.size(), target, conf, ans);
        return ans;
    }

private:
    void backTracking(
            const vector<int>& nums,
            int bgn, int end, int target,
            vector<int>& conf,
            vector<vector<int>>& ans) {

        if (target == 0) {
            ans.emplace_back(conf);
            return;
        }

        for (int i = bgn ; i < end ; ++i) {
            if (nums[i] > target) {
                break;
            }

            if (i > bgn && nums[i] == nums[i - 1]) {
                continue;
            }

            conf.emplace_back(nums[i]);
            backTracking(nums, i + 1, end, target - nums[i], conf, ans);
            conf.pop_back();
        }
    }
};
```