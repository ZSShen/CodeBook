
# Problem
### LeetCode 127. Word Ladder
https://leetcode.com/problems/word-ladder

# Solution
```c++
class Solution {
public:
    int ladderLength(string begin, string end, vector<string>& words) {

        /**
         *  TC: O(N * K * 25), where
         *      N is the number of words
         *      K is average word length
         *
         *  SC: O(N * K)
         *
         *              dot -- dog
         *            /            \
         *  hit -- hot              cog
         *            \            /
         *              lot -- log
         */

        unordered_set<string> dict(words.begin(), words.end());

        if (dict.count(end) == 0) {
            return 0;
        }

        queue<string> q;
        q.emplace(begin);

        int ans = 1;
        while (!q.empty()) {
            int n = q.size();
            ++ans;

            for (int i = 0 ; i < n ; ++i) {
                auto str = q.front();
                q.pop();

                int l = str.length();
                for (int j = 0 ; j < l ; ++j) {
                    char backup = str[j];

                    for (char ch = 'a' ; ch <= 'z' ; ++ch) {
                        str[j] = ch;

                        if (dict.count(str) == 0) {
                            continue;
                        }
                        if (str == end) {
                            return ans;
                        }

                        q.emplace(str);
                        dict.erase(str);
                    }

                    str[j] = backup;
                }
            }
        }

        return 0;
    }
};
```