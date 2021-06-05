
# Problem
### LeetCode 752. Open the Lock
https://leetcode.com/problems/open-the-lock

# Solution
```c++
class Solution {
public:
    int openLock(vector<string>& deadends, string target) {

        /**
         *  TC: O(N * D^N + S), where
         *      N is the length of the lock
         *      D is the number of digits
         *      S is the cost to convert deadend vector to set
         *
         *  So, we need to enumerate D^N combinations. Per each iteration, when
         *  generating new neighbors, the cost is O(N).
         *
         *  SC: O(D^N + S)
         */

        if (target == "0000") {
            return 0;
        }

        unordered_set<string> visit(deadends.begin(), deadends.end());
        if (visit.count("0000") == 1 || visit.count(target) == 1) {
            return -1;
        }
        visit.emplace("0000");

        queue<string> q;
        q.emplace("0000");

        int level = 0;

        while (!q.empty()) {
            int n = q.size();
            ++level;

            for (int i = 0 ; i < n ; ++i) {
                auto lock = q.front();
                q.pop();

                for (int j = 0 ; j < 4 ; ++j) {
                    char ch = lock[j];

                    // Rotate the wheel clockwise
                    lock[j] = ((ch - '0' + 1) % 10) + '0';
                    if (lock == target) {
                        return level;
                    }

                    if (visit.count(lock) == 0) {
                        q.emplace(lock);
                        visit.emplace(lock);
                    }
                    lock[j] = ch;

                    // Rotate the wheel counter clock-wise
                    lock[j] = ((ch - '0' + 9) % 10) + '0';
                    if (lock == target) {
                        return level;
                    }

                    if (visit.count(lock) == 0) {
                        q.emplace(lock);
                        visit.emplace(lock);
                    }
                    lock[j] = ch;
                }
            }
        }

        return -1;
    }
};
```