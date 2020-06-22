
# Problem
### LintCode 156. Merge Intervals
https://www.lintcode.com/problem/merge-intervals/description

# Solution
```c++
/**
 * Definition of Interval:
 * classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this->start = start;
 *         this->end = end;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param intervals: interval list.
     * @return: A new interval list.
     */
    vector<Interval> merge(vector<Interval> &intervals) {
        // write your code here

        sort(intervals.begin(), intervals.end(),
            [](const auto& lhs, const auto& rhs) {
            return lhs.start < rhs.start;
        });

        vector<Interval> ans;

        for (auto& interval : intervals) {
            if (ans.empty() || ans.back().end < interval.start) {
                ans.emplace_back(interval);
            } else {
                ans.back().end = max(ans.back().end, interval.end);
            }
        }

        return ans;s
    }
};
```
