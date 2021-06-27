
# Problem
### LeetCode 139. Word Break
https://leetcode.com/problems/word-break

# Solution
```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& words) {

        /**
         *  TC: O(N^3), where
         *      N is the string length
         *
         *  Improved TC: O(N * K * L), where
         *      N is the string length
         *      K is the number of dictionary words
         *      L is the average word length
         *
         *  SC: O(N)
         *
         *
         * dp[i]: Whether the prefix ending at the ith position can be composed
         *        by the dictionary words.
         *
         * dp[i] =   OR { dp[j] && (s.substr(j + 1, i) in dict) }
         *         0<=j<i
         *
         * Denote n as the length of s, and then the time complexity of this
         * baseline approach is O(n^3).
         *
         * In real implementation, we can further boost the performance by
         * enumerating the dictionary words in the inner loop. Suppose that
         * we have k words in total, and then the complexity of this approach
         * is O(n*k*l).
         *
         * S: 0 ...... i ......j
         * we have already calcuated the result for dp[i], and we enumerate
         * the dictionary words to predict the result for dp[j], where j > i.
         *
         */

        int n = s.length();
        vector<bool> dp(n + 1);
        dp[0] = true;

        for (int i = 0 ; i <= n ; ++i) {
            if (!dp[i]) {
                continue;
            }

            for (const auto& word : words) {
                int l = word.length();
                if (i + l > n) {
                    continue;
                }

                if (s.substr(i, l) != word) {
                    continue;
                }

                dp[i + l] = true;
            }
        }

        return dp[n] == true;
    }
};
```