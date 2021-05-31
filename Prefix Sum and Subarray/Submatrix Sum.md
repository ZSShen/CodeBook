
# Problem
### LintCode 405. Submatrix Sum
https://www.lintcode.com/problem/405

# Solution
```c++

class Solution {
public:
    /*
     * @param matrix: an integer matrix
     * @return: the coordinate of the left-up and right-down number
     */
    vector<vector<int>> submatrixSum(vector<vector<int>> &matrix) {
        // write your code here

        /**
         *  prefix(i) = array[0] + array[1] + ... + array[i];
         *  sum(i, j) = prefix(j) - prefix(i - 1)
         *  sum(i, j) = 0 => prefix(j) = prefix(i - 1)
         *
         *   a b c d      (a + b) -> A
         *   e f g h  =>  (e + f) -> B
         *   i j k l      (i + j) -> C
         *   m n o p      (m + n) -> D
         *
         *   Suppose that we want to scan the matrixes spanning from the
         *   first 2 columns, we can generate a synthetic column which merges
         *   these 2 columns and then apply the 1D solution we use to solve
         *   subarray sum problem to scan this synthetic column.
         *
         *   O(C^2 * R)
         */

        int m = matrix.size();
        int n = matrix[0].size();

        for (int i = 0 ; i < n ; ++i) {
            vector<int> syn(m);

            for (int j = i ; j < n ; ++j) {

                // Update the synthetic subarray.
                for (int k = 0 ; k < m ; ++k) {
                    syn[k] += matrix[k][j];
                }

                auto res = subarraySum(syn);
                if (res.first != -1 && res.second != -1) {
                    return {{res.first, i}, {res.second, j}};
                }
            }
        }

        return {{-1, -1}, {-1, -1}};
    }

private:
    pair<int, int> subarraySum(const vector<int>& nums) {

        unordered_map<int, int> map;
        map[0] = -1;

        int n = nums.size();
        int prefix = 0;

        for (int i = 0 ; i < n ; ++i) {
            prefix += nums[i];
            if (map.count(prefix) == 1) {
                return {map[prefix] + 1, i};
            }
            map[prefix] = i;
        }

        return {-1, -1};
    }
};
```