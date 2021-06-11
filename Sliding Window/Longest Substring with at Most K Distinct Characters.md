
# Problem
### LeetCode 340. Longest Substring with At Most K Distinct Characters
https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters

# Solution
```c++
class Solution {
public:
    int lengthOfLongestSubstringKDistinct(string s, int k) {

        /**
         *  TC: O(N), where
         *      N is the length of string s
         *
         *  SC: O(1)
         */

        vector<int> freq(128);
        int n = s.length(), ans = 0, count = 0, l = 0;

        for (int r = 0 ; r < n ; ++r) {
            char ch = s[r];
            ++freq[ch];

            if (freq[ch] == 1) {
                ++count;
            }

            while (l <= r && count > k) {
                ch = s[l++];
                --freq[ch];
                if (freq[ch] == 0) {
                    --count;
                }
            }

            ans = max(ans, r - l + 1);
        }

        return ans;
    }
};
```