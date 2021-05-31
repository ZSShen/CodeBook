
# Problem
### LeetCode 523. Continuous Subarray Sum
https://leetcode.com/problems/continuous-subarray-sum

# Solution
```c++
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  Classify prefix sums based on their remainders divided by k.
         *
         *  Also, since we concern the longer subarray (with size at least 2),
         *  we only record a prefix sum for its first occurrance. This makes
         *  sure that whenever we query `map[mod]`, we always get the minimal
         *  index, which helps enlarge the current subarray ending at index i.
         */

        unordered_map<int, int> map;

        // Set for the case that we have a prefix array sums up to a multiple
        // of k. sum(0, i) = nk.
        map[0] = -1;

        int mod = 0, n = nums.size();

        for (int i = 0 ; i < n ; ++i) {
            mod += nums[i];
            mod = (k != 0) ? mod % k : mod;

            if (map.count(mod) == 1) {
                if (i - map[mod] > 1) {
                    return true;
                }
            } else {
                map[mod] = i;
            }
        }

        return false;
    }
};
```