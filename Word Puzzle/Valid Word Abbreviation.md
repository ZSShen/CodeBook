
# Problem
### LintCode 637. Valid Word Abbreviation
https://www.lintcode.com/problem/valid-word-abbreviation/description

# Solution
```c++
class Solution {
public:
    /**
     * @param word: a non-empty string
     * @param abbr: an abbreviation
     * @return: true if string matches with the given abbr or false
     */
    bool validWordAbbreviation(string &word, string &abbr) {
        // write your code here

        int len_w = word.length();
        int len_a = abbr.length();

        int index_w = 0, index_a = 0;
        while (index_w < len_w && index_a < len_a) {

            if ('0' <= abbr[index_a] && abbr[index_a] <= '9') {

                if (abbr[index_a] == '0') {
                    break;
                }

                int num = 0;
                while ('0' <= abbr[index_a] && abbr[index_a] <= '9') {
                    num *= 10;
                    num += (abbr[index_a] - '0');
                    ++index_a;
                }

                index_w += num;
                continue;
            }

            if (abbr[index_a] != word[index_w]) {
                break;
            }

            ++index_w;
            ++index_a;
        }

        return (index_w == len_w) && (index_a == len_a);
    }
};
```
