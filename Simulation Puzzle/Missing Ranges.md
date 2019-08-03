
# Problem
### LintCode 641. Missing Ranges
https://www.lintcode.com/problem/missing-ranges/description

# Solution
```c++
class Solution {
public:
    /*
     * @param nums: a sorted integer array
     * @param lower: An integer
     * @param upper: An integer
     * @return: a list of its missing ranges
     */
    vector<string> findMissingRanges(vector<int> &nums, int lower, int upper) {
        // write your code here

        int n = nums.size();
        if (n == 0) {
            return {genRange(lower, upper)};
        }

        std::vector<std::string> ans;

        if (lower < nums[0]) {
            ans.push_back(genRange(lower, nums[0] - 1));
        }

        for (int i = 1 ; i < n ; ++i) {
            long diff = static_cast<long>(nums[i]) - nums[i - 1];
            if (diff <= 1) {
                continue;
            }
            ans.push_back(genRange(nums[i - 1] + 1, nums[i] - 1));
        }

        if (upper > nums[n - 1]) {
            ans.push_back(genRange(nums[n - 1] + 1, upper));
        }

        return ans;
    }

private:
    std::string genRange(long bgn, long end) {

        if (bgn == end) {
            return std::to_string(bgn);
        }

        return std::to_string(bgn) + "->" + std::to_string(end);
    }
};
```