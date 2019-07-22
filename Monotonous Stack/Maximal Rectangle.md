
# Problem
### LintCode 510. Maximal Rectangle
https://www.lintcode.com/problem/maximal-rectangle/description

# Solution
```c++
class Solution {
public:
    /**
     * @param matrix: a boolean 2D matrix
     * @return: an integer
     */
    int maximalRectangle(vector<vector<bool>> &matrix) {
        // write your code here

        /**
         *    Reduce the problem to find the maximal rectangle in a histogram.
         *
         *                                 *
         *    [1, 1, 0, 0, 1],             *
         *    [0, 1, 0, 0, 1],         * * *
         *    [0, 0, 1, 1, 1],  =>     * * *
         *    [0, 0, 1, 1, 1]      0 0 2 2 4
         *
         */

        int num_r = matrix.size();
        if (num_r == 0) {
            return 0;
        }

        int num_c = matrix[0].size();
        if (num_c == 0) {
            return 0;
        }

        int max = 0;
        std::vector<int> heights(num_c, 0);

        for (int i = 0 ; i < num_r ; ++i) {

            // Generate a new histogram.
            for (int j = 0 ; j < num_c ; ++j) {
                if (!matrix[i][j]) {
                    heights[j] = 0;
                } else {
                    ++heights[j];
                }
            }

            max = std::max(max, maximalRectangleInHistogram(num_c, heights));
        }

        return max;
    }


private:
    int maximalRectangleInHistogram(int n, const auto& heights) {

        int max = 0;
        std::stack<int> stk;

        for (int i = 0 ; i <= n ; ++i) {

            int curr = (i < n) ? heights[i] : -1;
            while (!stk.empty() && curr <= heights[stk.top()]) {

                int height = heights[stk.top()];
                stk.pop();

                int l = (!stk.empty()) ? stk.top() + 1 : 0;
                int r = i - 1;

                max = std::max(max, (r - l + 1) * height);
            }
            stk.push(i);
        }

        return max;
    }
};
```