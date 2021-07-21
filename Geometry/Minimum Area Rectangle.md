
# Problem
### LeetCode 939. Minimum Area Rectangle
https://leetcode.com/problems/minimum-area-rectangle

# Solution
```c++
class Solution {
public:
    int minAreaRect(vector<vector<int>>& points) {

        /**
         *  TC: O(N^2), where
         *      N is the number of points
         *
         *  SC: O(N)
         */

        unordered_map<int, unordered_set<int>> map;
        for (const auto& p : points) {
            map[p[0]].emplace(p[1]);
        }

        int n = points.size();
        int area = INT_MAX;

        for (int i = 0 ; i < n ; ++i) {
            for (int j = 0 ; j < n ; ++j) {
                if (i == j) {
                    continue;
                }

                const auto& a = points[i];
                const auto& b = points[j];

                if (a[0] == b[0] || a[1] == b[1]) {
                    continue;
                }

                if (map[a[0]].count(b[1]) == 0 ||
                    map[b[0]].count(a[1]) == 0) {
                    continue;
                }

                int w = abs(a[0] - b[0]);
                int h = abs(a[1] - b[1]);
                area = min(area, w * h);
            }
        }

        return area < INT_MAX ? area : 0;
    }
};
```