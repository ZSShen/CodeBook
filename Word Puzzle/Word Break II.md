
# Problem
### LintCode 582. Word Break II
https://www.lintcode.com/problem/word-break-ii/description

# Solution
```c++
class Solution {
public:
    /*
     * @param s: A string
     * @param wordDict: A set of words.
     * @return: All possible sentences.
     */
    vector<string> wordBreak(string &s, unordered_set<string> &wordDict) {
        // write your code here

        /**
         *  lintcode => l intcode
         *           => li ntcode
         *           => lin tcode
         *           => lint code
         *           ...
         *
         *  lint => l int   code => c ode
         *       => li nt        => co de
         *       => lin t        => cod e
         */

        if (s.empty()) {
            return {};
        }

        std::unordered_map<std::string, std::vector<std::string>> memo;
        return runBacktracking(s, wordDict, memo);
    }

private:
    std::vector<std::string> runBacktracking(
            const std::string& str,
            const std::unordered_set<std::string>& dict,
            std::unordered_map<std::string, std::vector<std::string>>& memo) {

        if (str.empty()) {
            return {""};
        }

        if (memo.count(str) == 1) {
            return memo[str];
        }

        std::vector<std::string> ans;

        int n = str.length();
        for (const auto& word : dict) {

            int l = word.length();
            if (l > n || l == 0) {
                continue;
            }

            auto prefix = str.substr(0, l);
            if (prefix != word) {
                continue;
            }

            auto suffix = str.substr(l, n - l);

            auto res = runBacktracking(suffix, dict, memo);

            /**
             * prefix:  piece:
             * a        b c d
             * a        bc d
             * a        bcd
             * ...
             */
            for (const auto& piece : res) {
                if (!piece.empty()) {
                    ans.push_back(prefix + " " + piece);
                } else {
                    ans.push_back(prefix);
                }
            }
        }

        memo[str] = std::move(ans);
        return memo[str];
    }
};
```