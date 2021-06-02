
# Problem
### LeetCode 161. One Edit Distance
https://leetcode.com/problems/one-edit-distance

# Solution
```c++
class Solution {
public:
    bool isOneEditDistance(string &s, string &t) {

        /**
         *  TC: O(S * T), where
         *      S is the length of string s
         *      T is the length of string t
         *
         *  SC: O(S + T)
         */

        int len_s = s.length();
        int len_t = t.length();

        int diff = std::abs(len_s - len_t);

        if (diff > 1) {
            return false;
        }

        if (diff == 0) {
            return checkStringsWithSameLength(s, t, len_s);
        }

        return checkStringsWithDifferentLength(s, t, len_s, len_t);
    }

private:
    bool checkStringsWithSameLength(
        const string& s, const string& t, int len) {

        int count = 0;

        for (int i = 0 ; i < len ; ++i) {
            if (s[i] != t[i]) {
                ++count;
                if (count == 2) {
                    return false;
                }
            }
        }

        return count == 1;
    }

    bool checkStringsWithDifferentLength(
        const string& s, const string& t, int len_s, int len_t) {

        int i = 0, j = 0;
        int count = 0;

        while (i < len_s && j < len_t) {
            if (s[i] == t[j]) {
                ++i;
                ++j;
                continue;
            }

            ++count;
            if (count == 2) {
                return false;
            }

            if (len_s > len_t) {
                ++i;
            } else {
                ++j;
            }
        }

        return true;
    }
};
```
