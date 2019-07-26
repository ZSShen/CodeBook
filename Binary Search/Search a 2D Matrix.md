
# Problem
### LintCode 28. Search a 2D Matrix
https://www.lintcode.com/problem/search-a-2d-matrix/description

# Solution
```c++
class Solution {
public:
    /**
     * @param matrix: matrix, a list of lists of integers
     * @param target: An integer
     * @return: a boolean, indicate whether matrix contains target
     */
    bool searchMatrix(vector<vector<int>> &matrix, int target) {
        // write your code here

        int num_r = matrix.size();
        if (num_r == 0) {
            return false;
        }

        int num_c = matrix[0].size();
        if (num_c == 0) {
            return false;
        }

        int r = determineRow(matrix, num_r, target);
        return searchRow(matrix[r], num_c, target);
    }

private:
    int determineRow(const auto& matrix, int num_r, int target) {

        int l = 0, r = num_r - 1;
        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (target >= matrix[m][0]) {
                l = m;
            } else {
                r = m;
            }
        }

        return (target >= matrix[r][0]) ? r : l;
    }

    bool searchRow(const auto& row, int num_c, int target) {

        int l = 0, r = num_c - 1;
        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (target >= row[m]) {
                l = m;
            } else {
                r = m;
            }
        }

        return (target == row[l] || target == row[r]) ? true : false;
    }
};
```