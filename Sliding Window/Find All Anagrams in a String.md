
# Problem
### LintCode 647. Find All Anagrams in a String
https://www.lintcode.com/problem/find-all-anagrams-in-a-string/description

# Solution
```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {

        int ls = s.length();
        int lp = p.length();

        if (ls < lp) {
            return {};
        }

        vector<int> freq_s(256, 0);
        int cnt_s = 0;

        vector<int> freq_t(256, 0);
        int cnt_t = 0;
        for (char ch : p) {
            ++freq_t[ch];
            if (freq_t[ch] == 1) {
                ++cnt_t;
            }
        }

        vector<int> ans;

        for (int i = 0 ; i < lp ; ++i) {
            char ch = s[i];
            ++freq_s[ch];
            if (freq_s[ch] == freq_t[ch]) {
                ++cnt_s;
            }
        }

        if (cnt_s == cnt_t) {
            ans.emplace_back(0);
        }

        int l = 0;
        for (int r = lp ; r < ls ; ++r) {
            char ch = s[r];

            // Add the new character pointed by r into the window.
            ++freq_s[ch];
            if (freq_s[ch] == freq_t[ch]) {
                ++cnt_s;
            }

            // Kick out the character pointed by l from the window.
            ch = s[l++];
            --freq_s[ch];
            if (freq_s[ch] == freq_t[ch] - 1) {
                --cnt_s;
            }

            if (cnt_s == cnt_t) {
                ans.emplace_back(l);
            }
        }

        return ans;
    }
};
```