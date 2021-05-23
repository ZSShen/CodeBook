
# Problem
### LeetCode 300. Longest Increasing Subsequence
https://leetcode.com/problems/longest-increasing-subsequence

# Solution
```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {

        /**
         *  TC: O(NlogN), where
         *      N is the number of elements.
         *
         *  SC: O(N)
         *
         *  L[i]: The length of the LIS ending at index i such that nums[i] is
         *        the last element of the LIS.
         *
         *  L[i] = | 1 + MAX{ L[j] }, where 0 < j < i and arr[j] < arr[i]
         *         | 1              , if no such j exists.
         *
         *
         *  example:
         *       4 2 4 5 3 7
         *
         *  lis [0] [1] [2] [3]
         *       4
         *       2   4
         *       2   4   5
         *       2   3   5
         *       2   3   5   7
         */

        vector<int> lis;
        lis.emplace_back(nums[0]);

        int n = nums.size();
        for (int i = 1 ; i < n ; ++i) {
            if (nums[i] > lis.back()) {
                lis.emplace_back(nums[i]);
                continue;
            }

            int l = 0, r = lis.size() - 1;
            while (l + 1 < r) {
                int m = l + (r - l) / 2;
                if (nums[i] <= lis[m]) {
                    r = m;
                } else {
                    l = m;
                }
            }

            if (nums[i] <= lis[l]) {
                lis[l] = nums[i];
            } else {
                lis[r] = nums[i];
            }
        }

        return lis.size();
    }
};
```