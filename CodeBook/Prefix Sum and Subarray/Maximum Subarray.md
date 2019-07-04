
# Problem
### LintCode 41. Maximum Subarray
https://www.lintcode.com/problem/maximum-subarray/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: A integer indicate the sum of max subarray
     */
    int maxSubArray(vector<int> &nums) {
        // write your code here

        int ans = nums[0];
        int local = 0;

        for (int num : nums) {
            local += num;

            ans = std::max(ans, local);

            if (local < 0) {
                local = 0;
            }
        }

        return ans;
    }
};
```