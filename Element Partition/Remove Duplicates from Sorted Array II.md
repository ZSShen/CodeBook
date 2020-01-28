
# Problem
### LintCode 101. Remove Duplicates from Sorted Array II
https://www.lintcode.com/problem/remove-duplicates-from-sorted-array-ii/description

# Solution
```c++
class Solution {
public:
    /**
     * @param A: a list of integers
     * @return : return an integer
     */
    int removeDuplicates(vector<int> &nums) {
        // write your code here

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        int l = 0;
        if (l < n - 1 && nums[l] == nums[l + 1]) {
            ++l;
        }

        for (int r = l + 1 ; r < n ; ++r) {
            if (nums[r] != nums[l]) {
                nums[++l] = nums[r];
                if (r < n - 1 && nums[r] == nums[r + 1]) {
                    nums[++l] = nums[++r];
                }
            }
        }

        return l + 1;
    }
};
```