
# Problem
### LintCode 405. Submatrix Sum
https://www.lintcode.com/problem/submatrix-sum/description

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

        int num_r = matrix.size();
        int num_c = matrix[0].size();

        for (int i = 0 ; i < num_c ; ++i) {

            std::vector<int> syn(num_r, 0);

            for (int j = i ; j < num_c ; ++j) {

                // Generate a new synthetic array.
                for (int k = 0 ; k < num_r ; ++k) {
                    syn[k] += matrix[k][j];
                }

                auto res = subarraySum(syn);
                if (res[0] == -1 && res[1] == -1) {
                    continue;
                }

                return {{res[0], i}, {res[1], j}};
            }
        }

        return {{-1, -1}, {-1, -1}};
    }

private:
    std::vector<int> subarraySum(
            const std::vector<int>& array) {

        int size = array.size();

        std::unordered_map<int, int> match;
        match[0] = -1;

        int sum = 0;
        for (int i = 0 ; i < size ; ++i) {

            sum += array[i];

            if (match.count(sum) == 0) {
                match[sum] = i;
            } else {
                return {match[sum] + 1, i};
            }
        }

        return {-1, -1};
    }

};
```