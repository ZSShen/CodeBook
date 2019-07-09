
# Problem
### LintCode 141. Sqrt(x)
https://www.lintcode.com/problem/sqrtx/description

# Solution
```c++
class Solution {
public:
    /**
     * @param x: An integer
     * @return: The sqrt of x
     */
    int sqrt(int x) {
        // write your code here

        int l = 1, r = x;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;

            int test = x / m;
            if (test >= m) {
                l = m;
            } else {
                r = m;
            }
        }

        return (r * r > x) ? l : r;
    }
};
```