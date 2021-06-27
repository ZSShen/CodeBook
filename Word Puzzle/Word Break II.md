
# Problem
### LeetCode 140. Word Break II
https://leetcode.com/problems/word-break-ii

# Solution
```c++
class Solution {
public:
    vector<string> wordBreak(string s, vector<string>& words) {

        unordered_set<string> dict(words.begin(), words.end());
        unordered_map<string, vector<string>> memo;
        return backTracking(s, dict, memo);
    }

private:
    vector<string> backTracking(
            const string& s,
            unordered_set<string>& dict,
            unordered_map<string, vector<string>>& memo) {

        if (s.empty()) {
            return {""};
        }

        if (memo.count(s) == 1) {
            return memo[s];
        }

        vector<string> ans;

        int n = s.length();
        for (int i = 0 ; i < n ; ++i) {
            auto prefix = s.substr(0, i + 1);
            if (dict.count(prefix) == 0) {
                continue;
            }

            auto suffix = s.substr(i + 1, n - i);
            auto res = backTracking(suffix, dict, memo);

            for (const auto& r : res) {
                if (r.empty()) {
                    ans.emplace_back(prefix);
                } else {
                    ans.emplace_back(prefix + " " + r);
                }
            }
        }

        return memo[s] = ans;
    }
};
```