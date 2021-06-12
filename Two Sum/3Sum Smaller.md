
# Problem
### LeetCode 259. 3Sum Smaller
https://leetcode.com/problems/3sum-smaller

# Solution
```c++
class Solution {
public:
    int threeSumSmaller(vector<int>& nums, int target) {

        /**
         *  TC: O(N^2), where
         *      N is the number of elements
         *
         *  SC: O(logN) to O(N), depending on the underlying sorting algorithm
         */

        int n = nums.size();
        sort(nums.begin(), nums.end());

        int ans = 0;

        for (int i = 0 ; i < n ; ++i) {
            target -= nums[i];

            int l = i + 1, r = n - 1;
            while (l < r) {
                if (nums[l] + nums[r] >= target) {
                    --r;
                } else {
                    ans += r - l;
                    ++l;
                }
            }

            target += nums[i];
        }

        return ans;
    }
};
```