
# Problem
### LeetCode 713. Subarray Product Less Than K
https://leetcode.com/problems/subarray-product-less-than-k

# Solution
```c++
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = nums.size();
        int ans = 0, l = 0, prod = 1;

        for (int r = 0 ; r < n ; ++r) {
            prod *= nums[r];

            while (prod >= k && l <= r) {
                prod /= nums[l++];
            }

            ans += r - l + 1;
        }

        return ans;
    }
};
```
