
# Problem
### LintCode 425. Letter Combinations of a Phone Number
https://www.lintcode.com/problem/letter-combinations-of-a-phone-number/description

# Solution
```c++
class Solution {
public:
    Solution()
      : map({
          {'2', {'a', 'b', 'c'}},
          {'3', {'d', 'e', 'f'}},
          {'4', {'g', 'h', 'i'}},
          {'5', {'j', 'k', 'l'}},
          {'6', {'m', 'n', 'o'}},
          {'7', {'p', 'q', 'r', 's'}},
          {'8', {'t', 'u', 'v'}},
          {'9', {'w', 'x', 'y', 'z'}}
      })
    { }

    vector<string> letterCombinations(string digits) {

        /**
         *  TC: O(4^N), where
         *      N is the string length
         *
         *  SC: O(N)
         */

        int n = digits.length();
        if (n == 0) {
            return {};
        }

        string config;
        vector<string> ans;

        runBacktracking(0, n, digits, config, ans);
        return ans;
    }

private:
    void runBacktracking(
            int i, int n,
            const string& digits,
            string& config,
            vector<string>& ans) {

        if (i == n) {
            ans.push_back(config);
            return;
        }

        for (char alphabet : map[digits[i]]) {
            config.push_back(alphabet);
            runBacktracking(i + 1, n, digits, config, ans);
            config.pop_back();
        }
    }

private:
    unordered_map<char, unordered_set<char>> map;
};
```