
# Problem
### LeetCode 290. Word Pattern
https://leetcode.com/problems/word-pattern

# Solution
```c++
class Solution {
public:
    bool wordPattern(string p, string s) {

        /**
         *  O(N), where
         *      N is the number of words
         *
         *  O(M), where
         *      M is the number of unique words
         */

        int np = p.length();
        istringstream in(s);

        unordered_map<char, string> p2s;
        unordered_map<string, char> s2p;

        int i = 0;
        for (string word ; in >> word ; ++i) {
            if (i == np) {
                return false;
            }

            char ch = p[i];
            if (p2s.count(ch) == 0) {
                p2s[ch] = word;
            } else {
                if (word != p2s[ch]) {
                    return false;
                }
            }

            if (s2p.count(word) == 0) {
                s2p[word] = ch;
            } else {
                if (ch != s2p[word]) {
                    return false;
                }
            }
        }

        return i == np;
    }
};
```