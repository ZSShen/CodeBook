
# Problem
### LeetCode 80. Remove Duplicates from Sorted Array II
https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii

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
        int l = 0;

        if (n > 1 && nums[l] == nums[l + 1]) {
            ++l;
        }

        for (int r = l + 1 ; r < n ; ++r) {
            if (nums[l] != nums[r]) {
                nums[++l] = nums[r];
                if (r + 1 < n && nums[r] == nums[r + 1]) {
                    nums[++l] = nums[++r];
                }
            }
        }

        return l + 1;
    }
};
```