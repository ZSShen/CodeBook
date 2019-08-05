
# Problem
### LintCode 627. Longest Palindrome
https://www.lintcode.com/problem/longest-palindrome/description

# Solution
```c++
class Solution {
public:
    /**
     * @param s: a string which consists of lowercase or uppercase letters
     * @return: the length of the longest palindromes that can be built
     */
    int longestPalindrome(string &s) {
        // write your code here

        std::vector<int> map(256, 0);
        for (char ch : s) {
            ++map[ch];
        }

        int len = 0;
        bool has_odd = false;
        for (int i = 0 ; i < 256 ; ++i) {
            if (map[i] == 0) {
                continue;
            }

            if (map[i] % 2 == 0) {
                len += map[i];
            } else {
                len += map[i] - 1;
                has_odd = true;
            }
        }

        return has_odd ? len + 1 : len;
    }
};
```
