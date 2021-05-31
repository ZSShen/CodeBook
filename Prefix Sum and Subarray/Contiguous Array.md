
# Problem
### LintCode 994. Contiguous Array
https://www.lintcode.com/problem/contiguous-array/description

# Solution
```c++
class Solution {
public:
    int findMaxLength(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  By converting 0 to -1, we transform the problem into finding
         *  the maximum size subarray that sums up to 0.
         */

        unordered_map<int, int> map;

        // Set up for the case that we have a prefix array sums up to 0.
        // sum(0, i) = 0.
        map[0] = -1;

        int prefix = 0, ans = 0, n = nums.size();

        for (int i = 0 ; i < n ; ++i) {
            int num = nums[i];
            if (num == 1) {
                ++prefix;
            } else {
                --prefix;
            }

            if (map.count(prefix) == 1) {
                ans = max(ans, i - map[prefix]);
            } else {
                map[prefix] = i;
            }
        }

        return ans;
    }
};
```