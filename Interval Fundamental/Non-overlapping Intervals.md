
# Problem
### LeetCode 435. Non-overlapping Intervals
https://leetcode.com/problems/non-overlapping-intervals

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
         */

        int n = intervals.size();
        if (n == 1) {
            return 0;
        }

        /**
         *  Why not sorting using the starting point of each interval?
         *
         *  Counter Example:
         *
         *      |--- B ---|  |-- C --|
         *
         *    |---------- A ----------|
         *
         */

        sort(intervals.begin(), intervals.end(),
             [] (const auto& l, const auto& r) {
                 return l[1] < r[1];
             });

        int ans = 0;
        int pivot = intervals[0][1];

        for (int i = 1 ; i < n ; ++i) {
            if (intervals[i][0] >= pivot) {
                pivot = intervals[i][1];
            } else {
                ++ans;
            }
        }

        return ans;
    }
};
```