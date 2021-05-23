
# Problem
### LeetCode 207. Course Schedule
https://leetcode.com/problems/course-schedule

# Solution
```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {

        /**
         * TC: O(V + E), where
         *      V is the number of nodes
         *      E is the number of edges
         *
         * SC: O(V + E)
         */

        unordered_map<int, unordered_set<int>> graph;
        unordered_map<int, int> indeg;

        for (const auto& p : prerequisites) {
            int s = p[0], t = p[1];
            ++indeg[t];
            graph[s].emplace(t);
        }

        queue<int> q;
        for (int i = 0 ; i < numCourses ; ++i) {
            if (indeg[i] == 0) {
                q.emplace(i);
            }
        }

        vector<int> order;

        while (!q.empty()) {
            int s = q.front();
            q.pop();
            order.emplace_back(s);

            for (int d : graph[s]) {
                --indeg[d];
                if (indeg[d] == 0) {
                    q.emplace(d);
                }
            }
        }

        return order.size() == numCourses;
    }
};
```