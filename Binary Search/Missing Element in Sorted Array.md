
# Problem
### LeetCode 1060. Missing Element in Sorted Array
https://leetcode.com/problems/missing-element-in-sorted-array/

# Solution
```c++
class Solution {
public:
    int missingElement(vector<int>& nums, int k) {

        /**
            L = 0, R = n - 1
            M = L + (R - L) / 2;

            # of numbers in [0, M] = nums[M] - nums[0] + 1
            # of missing numbers   = total - M - 1

            if (k <= #miss) {
                R = M
            } else {
                L = M
            }

            # of missing numbers before nums[L] = (nums[L] - nums[0] + 1) - (L + 1) = LO
            # of missing numbers before nums[R] = (nums[R] - nums[0] + 1) - (R + 1) = HI

            k in [LO, HI]  => nums[L] + (k - LO)
            k in (HI, INF) => nums[R] + (k - HI)
        */

        int n = nums.size();
        int l = 0, r = n - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;

            int total = nums[m] - nums[0] + 1;
            int miss = total - (m + 1);

            if (k <= miss) {
                r = m;
            } else {
                l = m;
            }
        }

        int lo = (nums[l] - nums[0] + 1) - (l + 1);
        int hi = (nums[r] - nums[0] + 1) - (r + 1);
        if (lo <= k && k <= hi) {
            return nums[l] + (k - lo);
        }
        return nums[r] + (k - hi);
    }
};
```