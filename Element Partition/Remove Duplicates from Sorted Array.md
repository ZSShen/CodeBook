
# Problem
### LeetCode 26. Remove Duplicates from Sorted Array
https://leetcode.com/problems/remove-duplicates-from-sorted-array/

# Solution
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        int l = 0, r = 0;

        while (r < n) {
            if (nums[r] != nums[l]) {
                ++l;
                nums[l] = nums[r];
            }
            ++r;
        }

        return l + 1;
    }
};
```