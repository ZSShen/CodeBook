
# Problem
### LeetCode 452. Minimum Number of Arrows to Burst Balloons
https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons

# Solution
```c++
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {

        /**
         *  TC: O(NlogN), where
         *      N is the number of intervals
         *
         *  SC: O(logN) to O(N), depending on the underlying sorting algorithm
         *

            [[10,16],[2,8],[1,6],[7,12]]

                     ------------

            -------
               ----------
                            --------
            -----------------------------
            1  2  6  7  8  10  12  16

            Must sort the ballons using the ending point.

            The counter example for sorting based on starting point.

              -----    -----
            -------------------

            sorting based on starting point: 1 arrow (wrong)
            sorting based on endint point: 2 arrows (correct)
         */

        sort(points.begin(), points.end(),
             [] (const auto& l, const auto& r) {
                return l[1] < r[1];
            });

        int ans = 1;
        int last = points[0][1];
        int n = points.size();

        for (int i = 1 ; i < n ; ++i) {
            if (points[i][0] > last) {
                ++ans;
                last = points[i][1];
            }
        }

        return ans;
    }
};
```