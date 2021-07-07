
# Problem
### LeetCode 398. Random Pick Index
https://leetcode.com/problems/random-pick-index

# Solution
```c++
class Solution {
public:
    Solution(vector<int>& nums)
        : nums(nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */
    }

    int pick(int target) {

        int n = nums.size(), count = 0;
        int ans;

        for (int i = 0 ; i < n ; ++i) {
            if (nums[i] == target) {
                ++count;
                if (random() % count == 0) {
                    ans = i;
                }
            }
        }

        return ans;
    }

private:
    vector<int> nums;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * int param_1 = obj->pick(target);
 */
```
