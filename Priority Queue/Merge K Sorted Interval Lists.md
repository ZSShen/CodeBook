
# Problem
### LintCode 577. Merge K Sorted Interval Lists

https://www.lintcode.com/problem/merge-k-sorted-interval-lists/description

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


struct Record {
    Interval interval;
    int id;
    int index;

    Record(Interval interval, int id, int index)
      : interval(interval), id(id), index(index)
    { }
};


struct RecordCompare {
    bool operator() (const auto& lhs, const auto& rhs) {
        if (lhs.interval.start == rhs.interval.end) {
            return lhs.interval.end > rhs.interval.end;
        }
        return lhs.interval.start > rhs.interval.start;
    }
};


class Solution {
public:
    /**
     * @param intervals: the given k sorted interval lists
     * @return:  the new sorted interval list
     */
    vector<Interval> mergeKSortedIntervalLists(vector<vector<Interval>> &intervals) {
        // write your code here

        std::priority_queue<Record, std::vector<Record>, RecordCompare> queue;
        int k = intervals.size();
        for (int i = 0 ; i < k ; ++i) {
            if (!intervals[i].empty()) {
                queue.push(Record(intervals[i][0], i, 0));
            }
        }

        // If all the interval lists are empty.
        if (queue.empty()) {
            return {};
        }

        auto rec = queue.top();
        queue.pop();

        auto prev = rec.interval;
        int id = rec.id;
        int index = rec.index;
        if (index < intervals[id].size() - 1) {
            queue.push(Record(intervals[id][index + 1], id, index + 1));
        }

        std::vector<Interval> ans;

        while (!queue.empty()) {
            rec = queue.top();
            queue.pop();

            auto curr = rec.interval;
            id = rec.id;
            index = rec.index;

            if (index < intervals[id].size() - 1) {
                queue.push(Record(intervals[id][index + 1], id, index + 1));
            }

            if (curr.start > prev.end) {
                ans.emplace_back(std::move(prev));
                prev = std::move(curr);
                continue;
            }

            prev.end = std::max(prev.end, curr.end);
        }
        ans.emplace_back(std::move(prev));

        return ans;
    }
};
```
