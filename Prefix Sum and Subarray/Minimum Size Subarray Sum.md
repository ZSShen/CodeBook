
# Problem
### LeetCode 209. Minimum Size Subarray Sum
https://leetcode.com/problems/minimum-size-subarray-sum

# Solution
```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         *
         *  Use 2 pointers, r and l, to scan the prefix sum array. In the
         *  procedure, r is the main pointer which controls the movement of
         *  our sliding window. In each iteration, when the subarray sum bounded
         *  by r and l, namely prefix[r] - prefix[l], is less than or eqaul to
         *  s, we try to adjust l so that we are able to get a smaller window
         *  that also fulfills the problem descpretion.
         *
         *  Note: In real implementation, we may use a single varable to
         *        represent the prefix sum array.
         *
         *    l
         *          r
         *  a b c d e f g h i
         *
         */

        int n = nums.size();
        int prefix = 0, l = 0, ans = INT_MAX;

        for (int r = 0 ; r < n ; ++r) {
            prefix += nums[r];

            while (prefix >= target && l <= r) {
                ans = min(ans, r - l + 1);
                prefix -= nums[l++];
            }
        }

        return ans < INT_MAX ? ans : 0;
    }
};
```