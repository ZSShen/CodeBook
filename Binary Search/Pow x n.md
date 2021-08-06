
# Problem
### LeetCode 50. Pow(x, n)
https://leetcode.com/problems/powx-n

# Solution
```c++
class Solution {
public:
    double myPow(double x, int n) {

        /**
         *  TC: O(logN), where
         *      N is the exponent
         *
         *  SC: O(logN)
         */

        long e = n;
        return (e >= 0) ? fastPow(x, e) : 1 / fastPow(x, -e);
    }

private:
    double fastPow(double x, long e) {

        if (e == 0) {
            return 1;
        }
        if (e == 1) {
            return x;
        }

        double res = fastPow(x, e >> 1);
        return (e % 2 == 0) ? res * res : res * res * x;
    }
};
```