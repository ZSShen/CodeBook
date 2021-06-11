
# Problem
### LeetCode 3. Longest Substring Without Repeating Characters
https://leetcode.com/problems/longest-substring-without-repeating-characters/

# Solution
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {

        /**
         *  TC: O(N), where
         *      N is the length of string s
         *
         *  SC: O(1)
         */

        vector<int> freq(128);
        int n = s.length(), ans = 0, l = 0;

        for (int r = 0 ; r < n ; ++r) {
            char ch = s[r];
            ++freq[ch];

            while (l <= r && freq[ch] > 1) {
                --freq[s[l++]];
            }

            ans = max(ans, r - l + 1);
        }

        return ans;
    }
};
```