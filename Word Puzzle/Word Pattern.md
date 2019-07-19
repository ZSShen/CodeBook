
# Problem
### LintCode 828. Word Pattern
https://www.lintcode.com/problem/word-pattern/description

# Solution
```c++
class Solution {
public:
    /**
     * @param pattern: a string, denote pattern string
     * @param teststr: a string, denote matching string
     * @return: an boolean, denote whether the pattern string and the matching string match or not
     */
    bool wordPattern(string &pattern, string &teststr) {
        // write your code here

        std::unordered_map<char, std::string> forward;
        std::unordered_map<std::string, char> backward;

        int bgn = 0, end = teststr.length();

        for (char ch : pattern) {
            auto token = getToken(teststr, bgn, end);
            if (token.empty()) {
                return false;
            }

            if (forward.count(ch) == 0) {
                forward[ch] = token;
            } else {
                if (forward[ch] != token) {
                    return false;
                }
            }

            if (backward.count(token) == 0) {
                backward[token] = ch;
            } else {
                if (backward[token] != ch) {
                    return false;
                }
            }
        }

        return true;
    }

private:
    std::string getToken(const std::string& str, int& bgn, int end) {

        if (bgn == end) {
            return "";
        }

        int curr = bgn;
        while (curr < end && str[curr] != ' ') {
            ++curr;
        }

        auto token = str.substr(bgn, curr - bgn);
        bgn = (curr < end) ? curr + 1 : curr;

        return token;
    }
};
```