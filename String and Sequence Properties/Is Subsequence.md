
# Problem
### LeetCode 392. Is Subsequence
https://leetcode.com/problems/is-subsequence

# Solution
```c++
class Solution {
public:
    bool isSubsequence(string s, string t) {

        /**
         *  TC: O(T), where
         *      T is the length of string t
         *
         *  SC: O(1)
         */

        int ls = s.length();
        int lt = t.length();

        int i = 0;
        for (int j = 0 ; i < ls && j < lt ; ++j) {
            if (s[i] == t[j]) {
                ++i;
            }
        }

        return i == ls;
    }
};
```
