
# Problem
### LeetCode 291. Word Pattern II
https://leetcode.com/problems/word-pattern-ii

# Solution
```c++
class Solution {
public:
    bool wordPatternMatch(string p, string s) {
        unordered_map<char, string> map;
        unordered_set<string> set;
        return backTracking(
            0, p.length(), 0, s.length(), p, s, map, set);
    }

private:
    bool backTracking(
            int ip, int np, int is, int ns,
            const string& p, const string& s,
            unordered_map<char, string>& map,
            unordered_set<string>& set) {

        if (ip == np && is == ns) {
            return true;
        }
        if (ip == np || is == ns) {
            return false;
        }

        char ch = p[ip];
        if (map.count(ch) == 1) {
            // The character has been mapped.

            const auto& token = map[ch];
            int l = token.length();

            if (is + l > ns) {
                return false;
            }
            if (token != s.substr(is, l)) {
                return false;
            }

            bool res = backTracking(
                ip + 1, np, is + l, ns, p, s, map, set);
            if (res) {
                return true;
            }
        } else {
            // Try to find a mapping for the character.

            for (int i = is ; i < ns ; ++i) {
                auto token = s.substr(is, i - is + 1);
                if (set.count(token) == 1) {
                    continue;
                }

                map[ch] = token;
                set.emplace(token);

                bool res = backTracking(
                    ip + 1, np, i + 1, ns, p, s, map, set);
                if (res) {
                    return true;
                }

                set.erase(token);
                map.erase(ch);
            }
        }

        return false;
    }
};
```