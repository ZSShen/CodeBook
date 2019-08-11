
# Problem
### LintCode 136. Palindrome Partitioning
https://www.lintcode.com/problem/palindrome-partitioning/description

# Solution
```c++
class Solution {
public:
    /*
     * @param s: A string
     * @return: A list of lists of string
     */
    vector<vector<string>> partition(string &s) {
        // write your code here

        int n = s.length();
        if (n == 0) {
            return {};
        }

        std::vector<std::string> collect;
        std::vector<std::vector<std::string>> ans;

        // Cache the substring str(i, j). If the substring is palindromic, we
        // cache its content. Otherwise, we cache a empty token.
        std::unordered_map<int, std::unordered_map<int, std::string>> memo;

        runBackTracking(s, 0, n, collect, ans, memo);

        return ans;
    }

private:
    void runBackTracking(
        const std::string& str,
        int index, int bound,
        std::vector<std::string>& collect,
        std::vector<std::vector<std::string>>& ans,
        std::unordered_map<int, std::unordered_map<int, std::string>>& memo) {

        if (index == bound) {
            ans.push_back(collect);
            return;
        }

        for (int i = index ; i < bound ; ++i) {

            std::string token;

            // Hit a cached record.
            if (memo.count(index) == 1 && memo[index].count(i) == 1) {
                token = memo[index][i];
                if (token.empty()) {
                    continue;
                }
            } else {
                token = str.substr(index, i - index + 1);
                if (!isPalindromic(token)) {
                    memo[index][i] = "";
                    continue;
                }
                memo[index][i] = token;
            }

            collect.push_back(token);
            runBackTracking(str, i + 1, bound, collect, ans, memo);
            collect.pop_back();
        }
    }

    bool isPalindromic(const std::string& str) {

        int len = str.length();
        int l = 0, r = len - 1;

        while (l < r) {
            if (str[l] != str[r]) {
                return false;
            }
            ++l;
            --r;
        }

        return true;
    }
};
```