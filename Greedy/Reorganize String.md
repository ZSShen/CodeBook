
# Problem
### LeetCode 767. Reorganize String
https://leetcode.com/problems/reorganize-string

# Solution
```c++
class Solution {
public:
    string reorganizeString(string s) {

        /**
         *  TC: O(N * log(26)), where
         *      N is the string length
         *
         *  SC: O(26)
         */

        vector<int> freq(26);
        for (char ch : s) {
            ++freq[ch - 'a'];
        }

        using T = pair<int, char>;
        priority_queue<T, vector<T>, less<>> q;
        for (int i = 0 ; i < 26 ; ++i) {
            if (freq[i] > 0) {
                q.push({freq[i], 'a' + i});
            }
        }

        string ans;

        while (!q.empty()) {
            auto a = q.top();
            q.pop();

            if (q.empty()) {
                if (a.first > 1) {
                    return "";
                } else {
                    ans.push_back(a.second);
                    break;
                }
            }

            auto b = q.top();
            q.pop();

            ans.push_back(a.second);
            ans.push_back(b.second);

            if (a.first > 1) {
                q.push({a.first - 1, a.second});
            }
            if (b.first > 1) {
                q.push({b.first - 1, b.second});
            }
        }

        return ans;
    }
};
```