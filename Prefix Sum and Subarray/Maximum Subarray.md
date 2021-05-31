
# Problem
### LeetCode 53. Maximum Subarray
https://leetcode.com/problems/maximum-subarray

# Solution
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {

        int ans = nums[0], sum = 0;

        for (int num : nums) {
            sum += num;
            ans = max(ans, sum);
            if (sum < 0) {
                sum = 0;
            }
        }

        return ans;
    }
};
```