
# Problem
### LeetCode 78. Subsets
https://leetcode.com/problems/subsets

# Solution
```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {

        /**
         *  TC: O(N * 2^N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         */

        vector<int> conf;
        vector<vector<int>> ans;

        int n = nums.size();
        for (int i = 0 ; i <= n ; ++i) {
            backTracking(nums, 0, n, 0, i, conf, ans);
        }

        return ans;
    }

private:
    void backTracking(
            const vector<int>& nums,
            int bgn, int end, int c, int n,
            vector<int>& conf,
            vector<vector<int>>& ans) {

        if (c == n) {
            ans.push_back(conf);
            return;
        }

        for (int i = bgn ; i < end ; ++i) {
            conf.emplace_back(nums[i]);
            backTracking(nums, i + 1, end, c + 1, n, conf, ans);
            conf.pop_back();
        }
    }
};
```