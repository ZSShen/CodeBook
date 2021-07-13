
# Problem
### LeetCode 33. Search in Rotated Sorted Array
https://leetcode.com/problems/search-in-rotated-sorted-array

# Solution
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {

        /**
         *  TC: O(logN), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int l = 0, r = nums.size() - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;

            if (nums[m] < nums[r]) {
                // The right portion is sorted.
                if (nums[m] <= target && target <= nums[r]) {
                    l = m;
                } else {
                    r = m;
                }
            } else {
                // The left portion is sorted.
                if (nums[l] <= target && target <= nums[m]) {
                    r = m;
                } else {
                    l = m;
                }
            }
        }

        if (nums[l] == target) {
            return l;
        }
        if (nums[r] == target) {
            return r;
        }
        return -1;
    }
};
```