
# Problem
### LeetCode 1306. Jump Game III
https://leetcode.com/problems/jump-game-iii

# Solution
```c++
class Solution {
public:
    bool canReach(vector<int>& arr, int start) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         */

        queue<int> q;
        q.emplace(start);

        int n = arr.size();
        vector<bool> visit(n);

        while (!q.empty()) {
            int src = q.front();
            q.pop();

            if (arr[src] == 0) {
                return true;
            }

            int dst = src + arr[src];
            if (dst < n && !visit[dst]) {
                q.emplace(dst);
                visit[dst] = true;
            }

            dst = src - arr[src];
            if (dst >= 0 && !visit[dst]) {
                q.emplace(dst);
                visit[dst] = true;
            }
        }

        return false;
    }
};
```