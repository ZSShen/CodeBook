
# Problem
### LeetCode 47. Permutations II
https://leetcode.com/problems/permutations-ii

# Solution
```c++
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {

        /**
         *  TC: O(N * N!), where
         *      N is the number of elements
         *
         *  SC: O(N)
         */

        sort(nums.begin(), nums.end());

        int n = nums.size();
        vector<bool> visit(n);
        vector<int> conf;
        vector<vector<int>> ans;

        backTracking(nums, 0, n, visit, conf, ans);
        return ans;
    }

private:
    void backTracking(
            const vector<int>& nums, int c, int n,
            vector<bool>& visit,
            vector<int>& conf,
            vector<vector<int>>& ans) {

        if (c == n) {
            ans.emplace_back(conf);
            return;
        }

        for (int i = 0 ; i < n ; ++i) {
            if (visit[i]) {
                continue;
            }
            if (i > 0 && nums[i] == nums[i - 1] && !visit[i - 1]) {
                continue;
            }

            visit[i] = true;
            conf.emplace_back(nums[i]);

            backTracking(nums, c + 1, n, visit, conf, ans);

            conf.pop_back();
            visit[i] = false;
        }
    }
};
```