
# Problem
### LeetCode 65. Valid Number
https://leetcode.com/problems/valid-number

# Solution
```c++
class Solution {
public:
    bool isNumber(string s) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(N)
         *
         *  Decompose the number format:
         *
         *  (): Include the necessary part.
         *  []: Include the optional part.
         *
         *  [+/-] (Real Number) [Exponent [+/-] (Integer)]
         *                                      *********
         *  Once we encounter a exponent symbol, then the remaining integer
         *  becomes necessary now.
         *
         *  Real Number: abcd
         *               abcd.ef
         *               abce.
         */

        s = trim(s);

        int n = s.length(), i = 0;
        s.push_back(' ');

        // Check for the optional -/+
        if (s[i] == '-' || s[i] == '+') {
            ++i;
        }

        int count_digit = 0, count_dot = 0;
        while (isdigit(s[i]) || s[i] == '.') {
            if (s[i] == '.') {
                ++count_dot;
            } else {
                ++count_digit;
            }
            ++i;
        }

        if (count_digit == 0 || count_dot > 1) {
            return false;
        }

        // Check for the optional e/E
        if (s[i] == 'e' || s[i] == 'E') {
            ++i;

            // Check for the optional -/+
            if (s[i] == '-' || s[i] == '+') {
                ++i;
            }

            int count_digit = 0;
            while (isdigit(s[i])) {
                ++count_digit;
                ++i;
            }

            if (count_digit == 0) {
                return false;
            }
        }

        return i == n;
    }

private:
    string trim(const string& s) {

        auto bgn = s.find_first_not_of(' ');
        if (bgn == string::npos) {
            return s;
        }

        auto end = s.find_last_not_of(' ');
        return s.substr(bgn, end - bgn + 1);
    }
};
```