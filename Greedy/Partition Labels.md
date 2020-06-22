
# Problem
### LeetCode 763. Partition Labels
https://leetcode.com/problems/partition-labels/

# Solution
```c++
class Solution {
public:
    vector<int> partitionLabels(string S) {
        /**
                            8           14        19
            a b a b c b a c a d e f e g d e h i j h k l i j

            last[a] = 8
            last[b] = 5
            last[c] = 7

            last[d] = 14
            last[e] = 15
            last[f] = 11
            last[g] = 13

            last[h] = 19
            last[i] = 22
            last[j] = 23
            last[k] = 20
        */

        int n = S.length();

        vector<int> last(26, 0);
        for (int i = 0 ; i < n ; ++i) {
            last[S[i] - 'a'] = i;
        }

        vector<int> ans;
        int window = 0;
        for (int i = 0, j = 0 ; i < n ; ++i) {
            window = max(window, last[S[i] - 'a']);
            if (window == i) {
                ans.emplace_back(i - j + 1);
                j = i + 1;
            }
        }

        return ans;
    }
};
```