
# Problem
### LintCode 386. Longest Substring with At Most K Distinct Characters
https://www.lintcode.com/problem/longest-substring-with-at-most-k-distinct-characters/description

# Solution
```c++
class Solution {
public:
    /**
     * @param s: A string
     * @param k: An integer
     * @return: An integer
     */
    int lengthOfLongestSubstringKDistinct(string &s, int k) {
        // write your code here

        int n = s.length();
        if (n == 0) {
            return 0;
        }

        std::vector<int> freq(256, 0);
        int count = 0;

        int max = 0;

        int l = 0;
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

            max = std::max(max, r - l + 1);
        }

        return max;
    }
};
```