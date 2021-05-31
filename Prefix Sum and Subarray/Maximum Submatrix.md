
# Problem
### LintCode 944. Maximum Submatrix
https://www.lintcode.com/problem/maximum-submatrix/description

# Solution
```c++


class Solution {
public:
    /**
     * @param matrix: the given matrix
     * @return: the largest possible sum
     */
    int maxSubmatrix(vector<vector<int>> &matrix) {
        // write your code here

        /**
         *  TC: O(R * (C^2)), where
         *      R is the number of rows
         *      C is the number of columns
         *
         *  SC: O(R * C)
         *
         *  i        j
         *  a1  b1  c1  d1      s1 (a1 + b1 + c1)
         *  a2  b2  c2  d2      s2
         *  a3  b3  c3  d3      s3                    s2    a2 b2 c2
         *  .   .   .   .    => .                 =>  .  => .  .  .
         *  .   .   .   .       .                     sk    ak bk ck
         *  an  bn  cn  dn      sn
         *
         */

        int m = matrix.size();
        if (m == 0) {
            return 0;
        }
        int n = matrix[0].size();
        if (n == 0) {
            return 0;
        }

        int max = matrix[0][0];

        for (int i = 0 ; i < n ; ++i) {
            std::vector<int> syn(m);

            for (int j = i ; j < n ; ++j) {

                // Update the synthetic array.
                for (int k = 0 ; k < m ; ++k) {
                    syn[k] += matrix[k][j];
                }

                int res = maxSubarray(syn);
                max = std::max(max, res);
            }
        }

        return max;
    }

private:
    int maxSubarray(const auto& nums) {

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