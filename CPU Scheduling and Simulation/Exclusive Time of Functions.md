
# Problem
### LeetCode 636. Exclusive Time of Functions
https://leetcode.com/problems/exclusive-time-of-functions

# Solution
```c++
class Solution {
public:
    vector<int> exclusiveTime(int n, vector<string>& logs) {

        /**
         *  TC: O(N), where
         *      N is the number of log records
         *
         *  SC: O(N)
         */

        stack<int> stack;
        char buf[8];
        int id, curr, prev;

        vector<int> ans(n);

        for (const auto& line : logs) {
            sscanf(line.c_str(), "%d:%[a-z]:%d", &id, buf, &curr);

            if (buf[0] == 's') {
                if (!stack.empty()) {
                    ans[stack.top()] += curr - prev;
                }
                prev = curr;
                stack.emplace(id);
            } else {
                ans[stack.top()] += curr - prev + 1;
                stack.pop();
                prev = curr + 1;
            }
        }

        return ans;
    }
};
```