
# Problem
### LeetCode 56. Merge Intervals
https://leetcode.com/problems/merge-intervals

# Solution
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {

        /**
         *  TC: O(NlogN), where
         *      N is the number of intervals
         *
         *  SC: O(logN) to O(N), depending on the underlying sorting algorithm
         */

        sort(intervals.begin(), intervals.end());

        vector<vector<int>> ans;
        auto pivot = intervals[0];

        int n = intervals.size();
        for (int i = 1 ; i < n ; ++i) {
            if (intervals[i][0] <= pivot[1]) {
                pivot[1] = max(pivot[1], intervals[i][1]);
            } else {
                ans.emplace_back(pivot);
                pivot = intervals[i];
            }
        }
        ans.emplace_back(pivot);

        return ans;
    }
};
```
