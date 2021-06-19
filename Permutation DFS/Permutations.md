
# Problem
### LeetCode 46. Permutations
https://leetcode.com/problems/permutations

# Solution
```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {

        /**
         *  TC: O(N * N!), where
         *      N is the number of elements
         *
         *  SC: O(N)
         */

        int n = nums.size();
        vector<bool> visit(n);
        vector<int> config;
        vector<vector<int>> ans;

        backTracking(nums, 0, n, visit, config, ans);
        return ans;
    }

private:
    void backTracking(
            const vector<int>& nums, int c, int n,
            vector<bool>& visit,
            vector<int>& config,
            vector<vector<int>>& ans) {

        if (c == n) {
            ans.push_back(config);
            return;
        }

        for (int i = 0 ; i < n ; ++i) {
            if (visit[i]) {
                continue;
            }

            visit[i] = true;
            config.push_back(nums[i]);
            backTracking(nums, c + 1, n, visit, config, ans);
            config.pop_back();
            visit[i] = false;
        }
    }
};
```