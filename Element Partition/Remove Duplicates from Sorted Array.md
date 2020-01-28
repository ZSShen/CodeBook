
# Problem
### LintCode 100. Remove Duplicates from Sorted Array
hhttps://www.lintcode.com/problem/remove-duplicates-from-sorted-array/description

# Solution
```c++
class Solution {
public:
    /*
     * @param nums: An ineger array
     * @return: An integer
     */
    int removeDuplicates(vector<int> &nums) {
        // write your code here

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        int l = 0;
        for (int r = 1 ; r < n ; ++r) {
            if (nums[r] == nums[l]) {
                continue;
            }
            nums[++l] = nums[r];
        }

        return l + 1;
    }
};
```