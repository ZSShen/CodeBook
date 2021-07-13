
# Problem
### LeetCode 153. Find Minimum in Rotated Sorted Array
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array

# Solution
```c++
class Solution {
public:
    int findMin(vector<int>& nums) {

        /**
         *  TC: O(logN), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = nums.size();
        int l = 0, r = n - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (nums[m] < nums[r]) {
                r = m;
            } else {
                l = m;
            }
        }

        return nums[l] < nums[r] ? nums[l] : nums[r];
    }
};
```