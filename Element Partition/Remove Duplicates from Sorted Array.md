
# Problem
### LeetCode 26. Remove Duplicates from Sorted Array
https://leetcode.com/problems/remove-duplicates-from-sorted-array

# Solution
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        int l = 0;

        for (int r = 1 ; r < n ; ++r) {
            if (nums[l] != nums[r]) {
                nums[++l] = nums[r];
            }
        }

        return l + 1;
    }
};
```