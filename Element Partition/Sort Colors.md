
# Problem
### LintCode 148. Sort Colors
https://www.lintcode.com/problem/sort-colors/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: A list of integer which is 0, 1 or 2
     * @return: nothing
     */
    void sortColors(vector<int> &nums) {
        // write your code here

        int n = nums.size();
        int zero = 0, one = 0, two = n - 1;

        /**
         * We use 3 pointers to track the elements:
         *
         *  1. The "one" pointer guides the scanning procedure.
         *  2. The "zero" pointer points to tail of the consecutive zeros, which
         *     are shifted to the left hand side of the array.
         *  3. The "two" pointer points to the tail of the consecutive twos,
         *     which are shifted to the right hand size of the array.
         *
         *       zero     two
         *          |     |
         *          v     v
         *  0 0 0 0 1 1 1 1 2 2 2 2
         */

        while (one <= two) {
            if (nums[one] == 0) {
                std::swap(nums[one], nums[zero]);
                ++zero;
                ++one;
            } else if (nums[one] == 2) {
                std::swap(nums[one], nums[two]);
                --two;
            } else {
                ++one;
            }
        }
    }
};
```