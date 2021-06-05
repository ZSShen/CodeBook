
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

            auto iter_f = forward.find(ch);
            if (iter_f == forward.end()) {
                forward[ch] = token;
            } else if (token != iter_f->second) {
                return false;
            }

            auto iter_b = backward.find(token);
            if (iter_b == backward.end()) {
                backward[token] = ch;
            } else if (ch != iter_b->second) {
                return false;
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