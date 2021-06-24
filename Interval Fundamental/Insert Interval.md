
# Problem
### LintCode 30. Insert Interval
https://www.lintcode.com/problem/insert-interval/description

# Solution
```c++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {

        /**
         *  TC: O(N), where
         *      N is the number of intervals
         *
         *  SC: O(1) to O(N), depending on whether we extend the original vector
         *                    when adding a new interval
         */

        auto it = intervals.begin();
        while (it != intervals.end()) {
            if ((*it)[0] >= newInterval[0]) {
                break;
            }
            ++it;
        }
        intervals.insert(it, newInterval);

        vector<vector<int>> ans;
        auto pivot = intervals[0];

        int n = intervals.size();
        for (int i = 0 ; i < n ; ++i) {
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
