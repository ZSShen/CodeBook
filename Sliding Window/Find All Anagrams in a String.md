
# Problem
### LeetCode 438. Find All Anagrams in a String
https://leetcode.com/problems/find-all-anagrams-in-a-string

# Solution
```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {

        /**
         *  TC: O(N), where
         *      N is the length of string s
         *
         *  SC: O(1)
         */

        vector<int> freq_s(128), freq_p(128);
        int unique = 0;
        for (char ch : p) {
            ++freq_p[ch];
            if (freq_p[ch] == 1) {
                ++unique;
            }
        }

        vector<int> ans;
        int ls = s.length(), lp = p.length();
        int l = 0, count = 0;

        for (int r = 0 ; r < ls ; ++r) {
            char ch = s[r];
            ++freq_s[ch];

            if (freq_s[ch] == freq_p[ch]) {
                ++count;
            }

            if (r - l == lp) {
                ch = s[l++];
                --freq_s[ch];
                if (freq_s[ch] == freq_p[ch] - 1) {
                    --count;
                }
            }

            if (count == unique) {
                ans.emplace_back(l);
            }
        }

        return ans;
    }
};
```