
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
         *  TC: O(NlogN), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  Sort the prefix sums and find the pair of the neighboring prefix
         *  sums that has the minimum gap.
         *
         *  s[0] = 0
         *  s[1] = nums[0]
         *  s[2] = nums[1] + s[1]
         *   .
         *   .
         *   .
         *  s[n] = nums[n - 1] + s[n - 1]
         *
         *  s[1], s[2], s[0], s[n - 1], ..., s[3]
         */

        // <key, value>
        // key   -> the prefix sum
        // value -> the ending index of the prefix sum
        vector<pair<int, int>> sums;
        sums.push_back({0, -1});

        int n = nums.size(), prefix = 0;
        for (int i = 0 ; i < n ; ++i) {
            prefix += nums[i];
            sums.push_back({prefix, i});
        }

        sort(sums.begin(), sums.end());

        int max_gap = INT_MAX;
        int bgn = 0, end = 0;
        for (int i = 1 ; i <= n ; ++i) {
            int gap = sums[i].first - sums[i - 1].first;
            if (gap >= max_gap) {
                continue;
            }
            max_gap = gap;
            bgn = min(sums[i].second, sums[i - 1].second) + 1;
            end = max(sums[i].second, sums[i - 1].second);
        }

        return {bgn, end};
    }
};
```