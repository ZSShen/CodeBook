
# Problem
### LeetCode 15. 3Sum
https://leetcode.com/problems/3sum

# Solution
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {

        /**
         *  TC: O(N^2), where
         *      N is the number of elements
         *
         *  SC: O(logN) to O(N), depending on the underlying sorting algorithm
         */

        sort(nums.begin(), nums.end());

        vector<vector<int>> ans;
        int n = nums.size();

        for (int i = 0 ; i < n - 2; ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }

            // Since the remaining numbers are all positive, it is impossible
            // to generate the legal triplets. We thus exit the loop here.
            if (nums[i] > 0) {
                break;
            }

            twoSum(nums, i + 1, n - 1, -nums[i], ans);
        }

        return ans;
    }

private:
    void twoSum(
            const vector<int>& nums,
            int l, int r, int t,
            vector<vector<int>>& ans) {

        while (l < r) {
            int sum = nums[l] + nums[r];
            if (sum == t) {
                ans.push_back({-t, nums[l], nums[r]});

                // Dedup
                while (++l < r && nums[l] == nums[l - 1]);
                while (--r > l && nums[r] == nums[r + 1]);
                continue;
            }

            if (sum > t) {
                while (--r > l && nums[r] == nums[r + 1]);
            } else {
                while (++l < r && nums[l] == nums[l - 1]);
            }
        }
    }
};
```