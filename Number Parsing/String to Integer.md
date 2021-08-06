
# Problem
### LeetCode 8. String to Integer (atoi)
https://leetcode.com/problems/string-to-integer-atoi

# Solution
```c++
class Solution {
public:
    int myAtoi(string str) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(1)
         */

        int n = str.length();
        int i = 0;

        // Skip the beginning white spaces.
        while (i < n && str[i] == ' ') {
            ++i;
        }

        if (i == n) {
            return 0;
        }

        // Check if the number if positive or negative.
        bool is_pos = true;
        if (str[i] == '-') {
            ++i;
            is_pos = false;
        } else if (str[i] == '+') {
            ++i;
        }

        // Extract the number.
        long num = 0;
        while (i < n && isdigit(str[i])) {
            num = num * 10 + str[i] - '0';

            if (num > INT_MAX) {
                break;
            }

            ++i;
        }

        if (!is_pos) {
            num = -num;
        }

        if (num < INT_MIN) {
            return INT_MIN;
        } else if (num > INT_MAX) {
            return INT_MAX;
        } else {
            return num;
        }
    }
};
```