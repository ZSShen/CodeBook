
# Problem
### LeetCode 442. Find All Duplicates in an Array
https://leetcode.com/problems/find-all-duplicates-in-an-array

# Solution
```c++
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {

        for (int num : nums) {
            nums[abs(num) - 1] *= -1;
        }

        vector<int> ans;

        for (int num : nums) {
            if (nums[abs(num) - 1] > 0) {
                ans.push_back(abs(num));
                nums[abs(num) - 1] *= -1;
            }
        }

        return ans;
    }
};
```