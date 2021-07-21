
# Problem
### LeetCode 1249. Minimum Remove to Make Valid Parentheses
https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses

# Solution
```c++
class Solution {
public:
    string minRemoveToMakeValid(string s) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(1)
         *
         *  l: # of to be checked '('
         *  r: # of to be checked ')'
         */

        int r = count(s.begin(), s.end(), ')'), l = 0;
        string ans;

        for (char ch : s) {
            if (ch == '(') {
                if (l == r) {
                    // Remove the extra open parenthesis.
                    continue;
                }
                ++l;
            } else if (ch == ')') {
                --r;
                if (l == 0) {
                    // Remove the extra close parenthesis.
                    continue;
                }
                --l;
            }

            ans.push_back(ch);
        }

        return ans;
    }
};
```