
# Problem
### LeetCode 560. Subarray Sum Equals K
https://leetcode.com/problems/subarray-sum-equals-k

# Solution
```c++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  sum(i, j) = prefix(j) - prefix(i - 1)
         *  => prefix(i - 1) = prefix(j) - sum(i, j)
         *  => prefix(i - 1) = prefix(j) - k
         */

        unordered_map<int, int> map;

        // Set for the case that we have a prefix array sums up to k.
        // sum(0, i) = k
        map[0] = 1;

        int ans = 0, prefix = 0;

        for (int num : nums) {
            prefix += num;
            ans += map[sum - k];
            ++map[prefix];
        }

        return ans;
    }
};
```