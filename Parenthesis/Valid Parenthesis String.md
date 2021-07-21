
# Problem
### LeetCode 678. Valid Parenthesis String
https://leetcode.com/problems/valid-parenthesis-string

# Solution
```c++
class Solution {
public:
    bool checkValidString(string s) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(1)
         */

        int max_diff = 0, min_diff = 0;

        for (char ch : s) {
            max_diff += (ch == '(' || ch == '*') ? 1 : -1;
            min_diff += (ch == ')' || ch == '*') ? -1 : 1;

            if (max_diff < 0) {
                return false;
            }
            min_diff = max(0, min_diff);
        }

        return min_diff == 0;
    }
};
```