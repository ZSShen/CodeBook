
# Problem
### LeetCode 452. Minimum Number of Arrows to Burst Balloons
https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/

# Solution
```c++
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {

        int n = points.size();
        if (n == 0) {
            return 0;
        }

        sort(points.begin(), points.end());

        int ans = 0;
        int base = points[0][1];

        for (int i = 1 ; i < n ; ++i) {
            // Extend the range of balloons that can be bursted by
            // an arrow.
            if (points[i][0] <= base) {
                base = min(base, points[i][1]);
                continue;
            }

            ++ans;
            base = points[i][1];
        }
        ++ans;

        return ans;
    }
};
```
