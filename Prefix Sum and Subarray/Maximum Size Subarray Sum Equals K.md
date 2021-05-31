
# Problem
### LintCode 911. Maximum Size Subarray Sum Equals k
https://www.lintcode.com/problem/maximum-size-subarray-sum-equals-k/description

# Solution
```c++
class Solution {
public:
    int maxSubArrayLen(vector<int>& nums, int k) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  sum(i, j) = prefix(j) - prefix(i - 1) = k
         *  => prefix(i - 1) = prefix(j) - k
         *
         *  Since we concern the longest subarray, we only record a prefix
         *  sum for its first occurrance. This makes sure that whenever
         *  we query `map[prefix - k]`, we always get the minimal index, which
         *  helps enlarge the current subarray ending at index i.
         */

        unordered_map<int, int> map;

        // Set up for the case that we have a prefix array sums up to k.
        // sum(0, i) = k.
        map[0] = -1;

        int prefix = 0, ans = 0, n = nums.size();

        for (int i = 0 ; i < n ; ++i) {
            prefix += nums[i];

            if (map.count(prefix - k) == 1) {
                ans = max(ans, i - map[prefix - k]);
            }
            if (map.count(prefix) == 0) {
                map[prefix] = i;
            }
        }

        return ans;
    }
};
```