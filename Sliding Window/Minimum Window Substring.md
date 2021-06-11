
# Problem
### LeetCode 76. Minimum Window Substring
https://leetcode.com/problems/minimum-window-substring

# Solution
```c++
class Solution {
public:
    string minWindow(string s, string t) {

        vector<int> freq_s(128), freq_t(128);
        int count_s = 0, count_t = 0;

        for (char ch : t) {
            ++freq_t[ch];
            if (freq_t[ch] == 1) {
                ++count_t;
            }
        }

        int ls = s.length(), bgn = -1, opt = INT_MAX, l = 0;

        for (int r = 0 ; r < ls ; ++r) {
            char ch = s[r];

            ++freq_s[ch];
            if (freq_s[ch] == freq_t[ch]) {
                ++count_s;
            }

            while (l <= r && count_s == count_t) {
                int len = r - l + 1;
                if (len < opt) {
                    opt = len;
                    bgn = l;
                }

                ch = s[l++];
                --freq_s[ch];
                if (freq_s[ch] == freq_t[ch] - 1) {
                    --count_s;
                }
            }
        }

        return bgn != -1 ? s.substr(bgn, opt) : "";
    }
};
```