
# Problem
### LeetCode 16. 3Sum Closest
https://leetcode.com/problems/3sum-closest

# Solution
```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {

        /**
         *  TC: O(N^2), where
         *      N is the number of elements
         *
         *  SC: O(logN) to O(N), depending on the underlying sorting algorithm
         */

        int n = nums.size();
        sort(nums.begin(), nums.end());

        int ans = 0, opt_diff = INT_MAX;

        for (int i = 0 ; i < n - 2 ; ++i) {
            target -= nums[i];
            int l = i + 1, r = n - 1;

            while (l < r) {
                int diff = nums[l] + nums[r] - target;
                int abs_diff = abs(diff);

                if (abs_diff < opt_diff) {
                    opt_diff = abs_diff;
                    ans = nums[l] + nums[r] + nums[i];
                }

                if (diff < 0) {
                    ++l;
                } else {
                    --r;
                }
            }

            target += nums[i];
        }

        return ans;
    }
};
```