
# Problem
### LintCode 539. Move Zeros
https://www.lintcode.com/problem/move-zeroes/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    void moveZeroes(vector<int> &nums) {
        // write your code here

        int n = nums.size();
        int l = 0, r = 0;

        while (r < n) {
            if (nums[r] != 0) {
                std::swap(nums[l], nums[r]);
                ++l;
            }
            ++r;
        }
    }
};
```