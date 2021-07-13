
# Problem
### LeetCode 81. Search in Rotated Sorted Array II
https://leetcode.com/problems/search-in-rotated-sorted-array-ii/

# Solution
```c++
class Solution {
public:
    bool search(vector<int>& nums, int target) {

        int l = 0;
        int r = nums.size() - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;

            if (nums[m] == target) {
                return true;
            }

            // The right portion is sorted.
            if (nums[m] < nums[r]) {
                if (nums[m] <= target && target <= nums[r]) {
                    l = m;
                } else {
                    r = m;
                }
                continue;
            }

            // The left portion is sorted.
            if (nums[m] > nums[r]) {
                if (nums[l] <= target && target <= nums[m]) {
                    r = m;
                } else {
                    l = m;
                }
                continue;
            }

            // A[m] == A[r] != target.
            --r;
        }

        return nums[l] == target || nums[r] == target;
    }
};
```