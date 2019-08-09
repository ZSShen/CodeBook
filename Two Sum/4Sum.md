
# Problem
### LintCode 58. 4Sum
https://www.lintcode.com/problem/4sum/description

# Solution
```c++
class Solution {
public:
    /**
     * @param numbers: Give an array
     * @param target: An integer
     * @return: Find all unique quadruplets in the array which gives the sum of zero
     */
    vector<vector<int>> fourSum(vector<int> &nums, int target) {
        // write your code here

        int n = nums.size();
        if (n == 0) {
            return {};
        }

        std::sort(nums.begin(), nums.end());

        std::vector<std::vector<int>> ans;

        for (int f = 0 ; f < n - 3 ; ++f) {
            if (f > 0 && nums[f] == nums[f - 1]) {
                continue;
            }

            for (int s = f + 1 ; s < n - 2 ; ++s) {
                if (s > f + 1 && nums[s] == nums[s - 1]) {
                    continue;
                }

                twoSum(nums, s + 1, n - 1, nums[f], nums[s], target, ans);
            }
        }

        return ans;
    }

private:
    void twoSum(
            const auto& nums, int bgn, int end,
            int first, int second, int target, auto& ans) {

        int l = bgn, r = end;
        int cache = first + second;

        while (l < r) {
            int sum = nums[l] + nums[r] + cache;
            if (sum == target) {
                ans.push_back({first, second, nums[l], nums[r]});

                while (++l < r && nums[l] == nums[l - 1]);
                while (l < --r && nums[r] == nums[r + 1]);

                continue;
            }

            if (sum > target) {
                while (l < --r && nums[r] == nums[r + 1]);
            } else {
                while (++l < r && nums[l] == nums[l - 1]);
            }
        }
    }
};
```
