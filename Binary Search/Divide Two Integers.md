
# Problem
### LeetCode 29. Divide Two Integers
https://leetcode.com/problems/divide-two-integers

# Solution
```c++
class Solution {
public:
    int divide(int dividend, int divisor) {

        /**
         *  TC: O(logN), where
         *      N is the dividend
         *
         *  SC: O(1)
         *
            dividend = 29, divisor = 4

            Round 1:
                divd = 29
                divr = 4

                step = 2
                => quot = 1 << 2 = 4

            Round 2:
                divd = 29 - 16 = 13
                divr = 4

                step = 1
                => quot = 1 << 1 = 2

            Round 3:
                divd = 13 - 8 = 5
                divr = 4

                step = 0
                => quot = 1 << 0 = 1

            Round 4:
                divd = 5 - 4 = 1
                divr = 4

            final quot = 7
        */

        long divd = abs(static_cast<long>(dividend));
        long divr = abs(static_cast<long>(divisor));

        long quot = 0;

        while (divd >= divr) {
            long step = 0;
            long temp = divr;

            while (temp << 1 <= divd) {
                ++step;
                temp <<= 1;
            }

            quot += 1L << step;
            divd -= temp;
        }

        if ((dividend < 0 && divisor > 0) ||
            (dividend > 0 && divisor < 0)) {
            quot = -quot;
        }

        return quot > INT_MAX ? INT_MAX : quot;
    }
};
```