
# Problem
### LintCode 120. Word Ladder
https://www.lintcode.com/problem/word-ladder/description

# Solution
```c++


struct Record {
    std::string word;
    int level;

    Record(const auto& word, int level)
      : word(word), level(level)
    { }
};


class Solution {
public:
    /*
     * @param start: a string
     * @param end: a string
     * @param dict: a set of string
     * @return: An integer
     */
    int ladderLength(string &start, string &end, unordered_set<string> &dict) {
        // write your code here

        /**
         *              dot -- dog
         *            /            \
         *  hit -- hot              cog
         *            \            /
         *              lot -- log
         */

        dict.emplace(end);

        queue<string> queue;
        queue.emplace(start);

        int step = 0;

        while (!queue.empty()) {
            ++step;
            int n = queue.size();

            for (int i = 0 ; i < n ; ++i) {
                auto str = queue.front();
                queue.pop();

                int l = str.length();
                for (int j = 0 ; j < l ; ++j) {
                    for (char ch = 'a' ; ch <= 'z' ; ++ch) {
                        char back = str[j];
                        str[j] = ch;

                        if (dict.count(str) == 0) {
                            str[j] = back;
                            continue;
                        }

                        if (str == end) {
                            return step + 1;
                        }

                        queue.emplace(str);
                        dict.erase(str);
                        str[j] = back;
                    }
                }
            }
        }

        return 0;
    }
};
```