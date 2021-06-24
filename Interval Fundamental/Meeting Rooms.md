
# Problem
### LeetCode 252. Meeting Rooms
https://leetcode.com/problems/meeting-rooms

# Solution
```c++
class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {

        /**
         *  TC: O(NlogN), where
         *      N is the number of intervals
         *
         *  SC: O(logN) to O(N), depending on the underlying sorting algorithm
         */

        int n = intervals.size();
        if (n == 0) {
            return true;
        }

        sort(intervals.begin(), intervals.end());

        for (int i = 1 ; i < n ; ++i) {
            if (intervals[i][0] < intervals[i - 1][1]) {
                return false;
            }
        }

        return true;
    }
};
```