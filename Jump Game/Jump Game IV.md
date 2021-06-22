
# Problem
### LeetCode 1345. Jump Game IV
https://leetcode.com/problems/jump-game-iv

# Solution
```c++
class Solution {
public:
    int minJumps(vector<int>& arr) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         */

        int n = arr.size();

        unordered_map<int, vector<int>> map;
        for (int i = 0 ; i < n ; ++i) {
            map[arr[i]].emplace_back(i);
        }

        vector<bool> visit(n);
        visit[0] = true;

        queue<int> queue;
        queue.emplace(0);

        int level = 0;

        while (!queue.empty()) {
            int size = queue.size();

            for (int i = 0 ; i < size ; ++i) {
                int src = queue.front();
                queue.pop();

                if (src == n - 1) {
                    return level;
                }

                if (src > 0 && !visit[src - 1]) {
                    queue.emplace(src - 1);
                    visit[src - 1] = true;
                }

                if (src < n - 1 && !visit[src + 1]) {
                    queue.emplace(src + 1);
                    visit[src + 1] = true;
                }

                int val = arr[src];
                for (int dst : map[val]) {
                    if (!visit[dst]) {
                        queue.emplace(dst);
                    }
                }

                // Please remember to remove it to avoid redundant checking
                // for large amount of the same number.
                // eg. [7,7,7,7,7,7,7,7,7,7,7,7,7,7...]
                map.erase(val);
            }

            ++level;
        }

        return -1;
    }
};
```