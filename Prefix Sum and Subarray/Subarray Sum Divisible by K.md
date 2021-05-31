
# Problem
### LeetCode 974. Subarray Sums Divisible by K
https://leetcode.com/problems/subarray-sums-divisible-by-k/

# Solution
```c++
class Solution {
public:
    int subarraysDivByK(vector<int>& nums, int k) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  Classify prefix sums based on their remainders divided by k.
         *
         *  nums: 4, 5, 0, -2, -3, 1
         *  k: 5
         *
         *  Prefixes  : 4, 9, 9, 7, 4, 5
         *  Remainders: 4, 4, 4, 2, 4, 0
         *
         *  Groups[0]:  1  1  1  1  1  2
         *  Groups[1]:  0  0  0  0  0  0
         *  Groups[2]:  0  0  1  1  1  1
         *  Groups[3]:  0  0  0  0  0  0
         *  Groups[4]:  1  2  3  3  4  4
         *
         *  Count:      0  1  3  3  6  1
         *
         */

        vector<int> groups(k);

        // Set for the case that we have a prefix array sums up to a multiple
        // of k. sum(0, i) = nk.
        groups[0] = 1;

        int ans = 0, prefix = 0;

        for (int num : nums) {
            prefix += num;
            prefix %= k;
            if (prefix < 0) {
                prefix += k;
            }

            ans += groups[prefix];
            ++groups[prefix];
        }

        return ans;
    }
};
```
