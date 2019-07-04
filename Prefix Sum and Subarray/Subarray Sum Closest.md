
# Problem
### LintCode 139. Subarray Sum Closest
https://www.lintcode.com/problem/subarray-sum-closest/description

# Solution
```c++


struct Record {
    int sum;
    int index;

    Record(int sum, int index)
      : sum(sum), index(index)
    { }
};


class Solution {
public:
    /*
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    vector<int> subarraySumClosest(vector<int> &nums) {
        // write your code here

        /**
         * Sort the prefix sums and find the pair of the neighboring prefix
         * sums that has the minimum gap.
         *
         * s[0] = 0
         * s[1] = nums[0]
         * s[2] = nums[1] + s[1]
         *  .
         *  .
         *  .
         * s[n] = nums[n - 1] + s[n - 1]
         *
         * s[1], s[2], s[0], s[n - 1], ..., s[3]
         */

        int n = nums.size();
        if (n == 0) {
            return {-1, -1};
        }

        std::vector<Record> prefix(n + 1, Record(0, -1));
        for (int i = 1 ; i <= n ; ++i) {
            prefix[i].sum = prefix[i - 1].sum + nums[i - 1];
            prefix[i].index = i - 1;
        }

        std::sort(prefix.begin(), prefix.end(),
            [](const auto& lhs, const auto& rhs) {
                return lhs.sum < rhs.sum;
            });

        int max_gap = INT_MAX;
        int bgn = 0, end = 0;

        for (int i = 1 ; i <= n ; ++i) {
            int gap = prefix[i].sum - prefix[i - 1].sum;
            if (gap < max_gap) {
                max_gap = gap;
                bgn = std::min(prefix[i].index, prefix[i - 1].index) + 1;
                end = std::max(prefix[i].index, prefix[i - 1].index);
            }
        }

        return {bgn, end};
    }
};
```