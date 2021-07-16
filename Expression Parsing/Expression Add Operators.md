
# Problem
### LeetCode 282. Expression Add Operators
https://leetcode.com/problems/expression-add-operators

# Solution
```c++
class Solution {
public:
    vector<string> addOperators(string num, int target) {

        /**
         *  TC: O(N * (3^N)), where
         *      N is the string length
         *
         *  SC: O(N)
         *
            1 2 3

            1 + 2

            exp              curr           prev   next_curr  next_prev
            1 + 2 + 3       3 + 3            2         6          3
            1 + 2 - 3       3 - 3            2         0         -3
            1 + 2 * 3       3 * 3 (X)
                            3 - 2 + 2 * 3    2         7          6
        */

        vector<string> ans;
        dfs(num, 0, num.length(), "", 0, 0, target, ans);
        return ans;
    }

private:
    void dfs(
        const string& str, int bgn, int end,
        const string& exp, int prev, int curr, int target,
        vector<string>& ans) {

        if (bgn == end) {
            if (curr == target) {
                ans.push_back(exp);
            }
            return;
        }

        for (int i = bgn ; i < end ; ++i) {

            // 0xxxxx
            if (i > bgn && str[bgn] == '0') {
                break;
            }

            auto op = str.substr(bgn, i - bgn + 1);
            long num = stol(op);
            if (num > INT_MAX) {
                break;
            }

            if (bgn == 0) {
                dfs(str, i + 1, end, op, num, num, target, ans);
                continue;
            }

            dfs(str, i + 1, end, exp + '+' + op,
                num, curr + num, target, ans);

            dfs(str, i + 1, end, exp + '-' + op,
                -num, curr - num, target, ans);

            dfs(str, i + 1, end, exp + '*' + op,
                prev * num, curr - prev + prev * num, target, ans);
        }
    }
};
```