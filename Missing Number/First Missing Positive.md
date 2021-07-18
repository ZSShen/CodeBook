
# Problem
### LeetCode 41. First Missing Positive
https://leetcode.com/problems/first-missing-positive

# Solution
```c++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = nums.size();

        bool has_one = false;
        for (int& num : nums) {
            if (num == 1) {
                has_one = true;
            } else if (num <= 0 || num > n) {
                num = 1;
            }
        }

        if (!has_one) {
            return 1;
        }

        for (int num : nums) {
            int key = abs(num) - 1;
            if (nums[key] > 0) {
                nums[key] = -nums[key];
            }
        }

        for (int i = 0 ; i < n ; ++i) {
            if (nums[i] > 0) {
                return i + 1;
            }
        }

        return n + 1;
    }
};
```