
# Problem
### LeetCode 287. Find the Duplicate Number
https://leetcode.com/problems/find-the-duplicate-number

# Solution
```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int slow = nums[0], fast = nums[0];

        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }

        return slow;
    }
};
```
