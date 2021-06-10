
# Problem
### LeetCode 1086. High Five
https://leetcode.com/problems/high-five

# Solution
```c++
class Solution {
public:
    vector<vector<int>> highFive(vector<vector<int>>& items) {

        /**
         *  TC: O(N * log5), where
         *      N is the number of items
         *
         *  SC: O(N)
         */

        unordered_map<int, priority_queue<int, vector<int>, greater<int>>> map;

        for (const auto& item : items) {
            int id = item[0];
            int score = item[1];

            map[id].emplace(score);
            if (map[id].size() > 5) {
                map[id].pop();
            }
        }

        vector<vector<int>> ans;

        for (auto& entry : map) {
            int id = entry.first;
            int score = 0;

            auto& queue = entry.second;
            int size = queue.size();

            while (!queue.empty()) {
                score += queue.top();
                queue.pop();
            }

            ans.push_back({id, score / size});
        }

        sort(ans.begin(), ans.end());

        return ans;
    }
};
```
