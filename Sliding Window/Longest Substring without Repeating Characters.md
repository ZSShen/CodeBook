
# Problem
### LintCode 384. Longest Substring Without Repeating Characters
https://www.lintcode.com/problem/longest-substring-without-repeating-characters/description

# Solution
```c++
class Solution {
public:
    /**
     * @param s: a string
     * @return: an integer
     */
    int lengthOfLongestSubstring(string &s) {
        // write your code here

        int n = s.length();
        if (n == 0) {
            return 0;
        }

        std::vector<bool> bag(256, false);
        int l = 0, r = 0;
        int ans = 0;

        while (r < n) {
            char ch = s[r];

            if (!bag[ch]) {
                bag[ch] = true;

                // Update the maximum window size here.
                ans = std::max(ans, r - l + 1);
            } else {
                while (s[l] != ch) {
                    bag[s[l]] = false;
                    ++l;
                }
                ++l;
            }

            ++r;
        }

        return ans;
    }
};
```