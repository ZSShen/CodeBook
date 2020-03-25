
# Problem
### LintCode 1263. Is Subsequence
https://www.lintcode.com/problem/is-subsequence/description

# Solution
```c++
class Solution {
public:
    /**
     * @param s: the given string s
     * @param t: the given string t
     * @return: check if s is subsequence of t
     */
    bool isSubsequence(string &s, string &t) {
        // Write your code here

        int len_s = s.length();
        int len_t = t.length();

        int j = 0;
        for (int i = 0 ; i < len_t && j < len_s ; ++i) {
            if (s[j] == t[i]) {
                ++j;
            }
        }

        return j == len_s;
    }
};
```
