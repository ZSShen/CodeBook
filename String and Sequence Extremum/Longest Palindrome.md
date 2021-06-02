
# Problem
### LeetCode 409. Longest Palindrome
https://leetcode.com/problems/longest-palindrome

# Solution
```c++
class Solution {
public:
    int longestPalindrome(string s) {

        vector<int> freq(128, 0);
        for (char ch : s) {
            ++freq[ch];
        }

        int len = 0;
        bool has_odd = false;
        for (int f : freq) {
            if (f % 2 == 1) {
                has_odd = true;
                len += f - 1;
            } else {
                len += f;
            }
        }

        if (has_odd) {
            ++len;
        }
        return len;
    }
};
```
