
# Problem
### LeetCode 548. Split Array with Equal Sum
https://leetcode.com/problems/split-array-with-equal-sum

# Solution
```c++
class Solution {
public:
    bool splitArray(vector<int>& nums) {

        /**
         *  TC: O(N^2), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  n = 7
         *
         *  input array:
         *          i   j   k
         *       [1,2,1,2,1,2,1]
         *
         *  prefix:
         *
         *     [0,1,2,1,2,1,2,1]
         *      0 1 2 3 4 5 6 7
         *
         */

        int n = nums.size();

        vector<int> prefix(n + 1);
        for (int i = 1 ; i <= n ; ++i) {
            prefix[i] = prefix[i - 1] + nums[i - 1];
        }

        for (int j = 4 ; j < n - 2 ; ++j) {
            unordered_set<int> cache;

            for (int i = 2 ; i < j - 1 ; ++i) {
                int l = prefix[i - 1];
                int r = prefix[j - 1] - prefix[i];
                if (l == r) {
                    cache.emplace(r);
                }
            }

            for (int k = j + 2 ; k < n ; ++k) {
                int l = prefix[k - 1] - prefix[j];
                int r = prefix[n] - prefix[k];
                if (l == r && cache.count(l) == 1) {
                    return true;
                }
            }
        }

        return false;
    }
};
```