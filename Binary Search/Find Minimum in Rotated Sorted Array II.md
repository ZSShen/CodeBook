
# Problem
### LeetCode 154. Find Minimum in Rotated Sorted Array II
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii

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
            } else if (nums[m] > nums[r]) {
                l = m;
            } else {
                --r;
            }
        }

        return min(nums[l], nums[r]);
    }
};
```