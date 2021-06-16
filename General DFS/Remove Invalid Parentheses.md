
# Problem
### LeetCode 301. Remove Invalid Parentheses
https://leetcode.com/problems/remove-invalid-parentheses

# Solution
```c++
class Solution {
public:
    vector<string> removeInvalidParentheses(string s) {

        /**
         *  TC: O(2^N), where
         *       N is the string length
         *
         *  SC: O(N)
         */

        int l = 0, r = 0;
        for (char ch : s) {
            if (ch == '(') {
                ++l;
            } else if (ch == ')') {
                if (l > 0) {
                    --l;
                } else {
                    ++r;
                }
            }
        }

        vector<string> ans;
        backTracking(s, 0, s.length(), l, r, ans);
        return ans;
    }

private:
    bool isValid(const string& s) {

        int l = 0, r = 0;
        for (char ch : s) {
            if (ch == '(') {
                ++l;
            } else if (ch == ')') {
                if (l > 0) {
                    --l;
                } else {
                    ++r;
                }
            }
        }
        return l == 0 && r == 0;
    }

    void backTracking(
            const string& s,
            int bgn, int end, int l, int r,
            vector<string>& ans) {

        if (l == 0 && r == 0) {
            if (isValid(s)) {
                ans.push_back(s);
            }
            return;
        }

        for (int i = bgn ; i < end ; ++i) {

            // We should consider a case that may generate duplicates, like
            // "(()" => "()" "()"
            if (i > bgn && s[i] == s[i - 1]) {
                continue;
            }

            if (s[i] == '(' && l > 0) {
                auto copy(s);
                copy.erase(i, 1);
                backTracking(copy, i, end - 1, l - 1, r, ans);
            }
            if (s[i] == ')' && r > 0) {
                auto copy(s);
                copy.erase(i, 1);
                backTracking(copy, i, end - 1, l, r - 1, ans);
            }
        }
    }
};
```