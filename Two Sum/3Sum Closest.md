
# Problem
### LintCode 59. 3Sum Closest
https://www.lintcode.com/problem/3sum-closest/description

# Solution
```c++
class Solution {
public:
    /**
     * @param numbers: Give an array numbers of n integer
     * @param target: An integer
     * @return: return the sum of the three integers, the sum closest target.
     */
    int threeSumClosest(vector<int> &nums, int target) {
        // write your code here

        int n = nums.size();
        if (n == 0) {
            return 0;
        }

        std::sort(nums.begin(), nums.end());

        int min_diff = INT_MAX;
        int ans;

        for (int f = 0 ; f < n - 2 ; ++f) {

            if (f > 0 && nums[f] == nums[f - 1]) {
                continue;
            }

            int l = f + 1;
            int r = n - 1;
            while (l < r) {
                int sum = nums[f] + nums[l] + nums[r];
                int diff = sum - target;

                int abs_diff = std::abs(diff);
                if (abs_diff < min_diff) {
                    min_diff = abs_diff;
                    ans = sum;
                }

                if (diff > 0) {
                    while (l < --r && nums[r] == nums[r + 1]);
                } else {
                    while (++l < r && nums[l] == nums[l - 1]);
                }
            }
        }

        return ans;
    }
};
```