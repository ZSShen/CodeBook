
# Problem
### LintCode 8. Rotate String
https://www.lintcode.com/problem/rotate-string/description

# Solution
```c++
class Solution {
public:
    /**
     * @param str: An array of char
     * @param offset: An integer
     * @return: nothing
     */
    void rotateString(string &str, int offset) {
        // write your code here

        int n = str.length();

        if (offset == 0 || n == 0) {
            return;
        }

        int r = n - (offset % n);

        /**
         *  a b c d e f g
         *
         *  offset = 3
         *  r = n - offset = 4
         *
         *  (a b c d) (e f g)
         *  (d c b a) (g f e)
         * => e f g a b c d
         *
         */

        std::reverse(str.begin(), str.begin() + r);
        std::reverse(str.begin() + r, str.end());
        std::reverse(str.begin(), str.end());
    }
};
```