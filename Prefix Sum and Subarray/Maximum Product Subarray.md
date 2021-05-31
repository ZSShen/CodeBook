
# Problem
### Leetcode 152. Maximum Product Subarray
https://leetcode.com/problems/maximum-product-subarray/

# Solution
```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         *
         *       nums:    2, 3, -2,  4
         *
         *  min_sofar: 1  2  3 -12 -48
         *  max_sofar: 1  2  6  -2   4
         *
         *
         *       nums:    2, 3, -1,  4, -4
         *
         *  min_sofar: 1  2  3  -6 -24 -16
         *  max_sofar: 1  2  6  -1   4  96
         */

        int min_sofar = 1, max_sofar = 1;
        int ans = nums[0];

        for (int num : nums) {
            int min_curr = min(min(num, min_sofar * num), max_sofar * num);
            int max_curr = max(max(num, min_sofar * num), max_sofar * num);

            ans = max(ans, max_curr);
            min_sofar = min_curr;
            max_sofar = max_curr;
        }

        return ans;
    }
};
```