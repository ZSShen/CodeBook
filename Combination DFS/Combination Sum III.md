
# Problem
### LeetCode 216. Combination Sum III
https://leetcode.com/problems/combination-sum-iii

# Solution
```c++
class Solution {
public:
    vector<vector<int>> combinationSum3(int k, int n) {

        /**
         *  TC: O(C(9, K)), where
         *      K is the required amount of numbers
         *
         *  SC: O(K)
         */

        vector<int> conf;
        vector<vector<int>> ans;
        backTracking(1, 10, 0, k, n, conf, ans);
        return ans;
    }

private:
    void backTracking(
            int bgn, int end, int c, int k, int n,
            vector<int>& conf,
            vector<vector<int>>& ans) {

        if (c == k) {
            if (n == 0) {
                ans.emplace_back(conf);
            }
            return;
        }

        for (int i = bgn ; i < end ; ++i) {
            if (i > n) {
                break;
            }

            conf.emplace_back(i);
            backTracking(i + 1, end, c + 1, k, n - i, conf, ans);
            conf.pop_back();
        }
    }
};
```