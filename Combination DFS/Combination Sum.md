
# Problem
### LeetCode 39. Combination Sum
https://leetcode.com/problems/combination-sum

# Solution
```c++
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& nums, int target) {

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

            conf.emplace_back(nums[i]);
            backTracking(nums, i, end, target - nums[i], conf, ans);
            conf.pop_back();
        }
    }
};
```