
# Problem
### LeetCode 268. Missing Number
https://leetcode.com/problems/missing-number

# Solution
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = nums.size();
        int miss = n * (n + 1) / 2;

        for (int num : nums) {
            miss -= num;
        }

        return miss;
    }
};
```