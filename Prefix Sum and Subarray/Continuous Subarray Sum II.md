
# Problem
### LintCode 403. Continuous Subarray Sum II
https://www.lintcode.com/problem/continuous-subarray-sum-ii/description?_from=ladder&&fromId=4

# Solution
```c++
struct Record {
    int bgn, end, sum;

    Record(int bgn, int end, int sum)
      : bgn(bgn), end(end), sum(sum)
    { }
};


class Solution {
public:
    /*
     * @param A: An integer array
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    vector<int> continuousSubarraySumII(vector<int> &A) {
        // write your code here

        /**
         *  Denote the maximum subarray as S(i, j).
         *  Then, we need to handle 2 scenarios.
         *
         *  1. i < j, implying that the subarray locates in a normal range, or
         *     non-cyclic range.
         *
         *  2. i > j, implying that the subarray exceeds the boundary of the
         *     input array, thus spanning a cyclic range. However, this also
         *     implies that the minimum subarray locates in a normal range.
         *     Thus, to get the maximum subarray, we can subract the total
         *     sum of the input array with the minimum subarray.
         *
         *  Finally, compare the results generated in the aforementioned 2
         *  scenarios to get the real maximum subarray.
         *
         *  e.g:
         *
         *       S0
         *
         * Sn-1       S1     => S1 -> Si (i <= n - 1) Normal range
         *                   => Sj -> S2 (j <= n - 1) Cyclic range
         *     S3   S2
         *
         */

        int n = A.size();
        if (n == 0) {
            return {-1, -1};
        }

        int total = 0;
        for (int num : A) {
            total += num;
        }

        auto max = findMax(A, n);
        auto min = findMin(A, n);

        if (max.sum > total - min.sum) {
            return {max.bgn, max.end};
        }

        // All the array numbers are negative.
        if (min.bgn == 0 && min.end == n - 1) {
            return {max.bgn, max.end};
        }

        int bgn = min.end + 1;
        if (bgn == n) {
            bgn = 0;
        }

        int end = min.bgn - 1;
        if (end == -1) {
            end = n - 1;
        }

        return {bgn, end};
    }

private:
    Record findMax(const std::vector<int>& nums, int n) {

        int max = nums[0], max_bgn = 0, max_end = 0;
        int sum = 0, bgn = 0, end = 0;

        while (end < n) {
            sum += nums[end];

            if (sum > max) {
                max = sum;
                max_bgn = bgn;
                max_end = end;
            }

            ++end;

            if (sum < 0) {
                sum = 0;
                bgn = end;
            }
        }

        return Record(max_bgn, max_end, max);
    }

    Record findMin(const std::vector<int>& nums, int n) {

        int min = nums[0], min_bgn = 0, min_end = 0;
        int sum = 0, bgn = 0, end = 0;

        while (end < n) {
            sum += nums[end];

            if (sum < min) {
                min = sum;
                min_bgn = bgn;
                min_end = end;
            }

            ++end;

            if (sum > 0) {
                sum = 0;
                bgn = end;
            }
        }

        return Record(min_bgn, min_end, min);
    }
};
```