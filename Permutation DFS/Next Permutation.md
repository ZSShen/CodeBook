
# Problem
### LeetCode 31. Next Permutation
https://leetcode.com/problems/next-permutation

# Solution
```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         *
         *  From right to left, the numbers are sorted in
         *  monotonous non-decreasing order
         *
         *        turning point
         *          |
         *          v
         *      1 2 5 4 3 1
         *          ^^^^^^^
         *
         *      1 3 4 5 2 1
         *          ^^^^^^^
         *                   Reverse the right portion
         *      1 3 1 2 4 5
         *          ^^^^^^^
         */

        int n = nums.size();

        // Find the turning point.
        int i;
        for (i = n - 1 ; i > 0 ; --i) {
            if (nums[i - 1] < nums[i]) {
                break;
            }
        }
        --i;

        // The input is already the maximum permutation.
        if (i < 0) {
            reverse(nums.begin(), nums.end());
            return;
        }

        // Find the greater element on the right-hand side.
        int j;
        for (j = n - 1 ; j > i ; --j) {
            if (nums[j] > nums[i]) {
                break;
            }
        }

        // Swap the two numbers.
        swap(nums[i], nums[j]);

        // Revese the right-hand side.
        reverse(nums.begin() + i + 1, nums.end());
    }
};
```