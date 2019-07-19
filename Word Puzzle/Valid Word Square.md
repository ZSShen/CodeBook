
# Problem
### LintCode 888. Valid Word Square
https://www.lintcode.com/problem/valid-word-square/description

# Solution
```c++
class Solution {
public:
    /**
     * @param words: a list of string
     * @return: a boolean
     */
    bool validWordSquare(vector<string> &words) {
        // Write your code here

        int num_r = words.size();

        for (int i = 0 ; i < num_r ; ++i) {

            int num_c = words[i].length();
            if (num_c != num_r) {
                return false;
            }

            for (int j = 0 ; j < num_c ; ++j) {
                if (words[i][j] != words[j][i]) {
                    return false;
                }
            }
        }

        return true;
    }
};
```