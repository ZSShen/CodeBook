
# Problem
### LintCode 919. Meeting Rooms II
https://www.lintcode.com/problem/meeting-rooms-ii/description

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
    int time;
    char type;

    Record(int time, char type)
      : time(time), type(type)
    { }
};


class Solution {
public:
    /**
     * @param intervals: an array of meeting time intervals
     * @return: the minimum number of conference rooms required
     */
    int minMeetingRooms(vector<Interval> &intervals) {
        // Write your code here

        /**
         *
         *    ****  ****
         *
         *  ******************
         *
         *  0 5 10 15 20 25 30
         *
         */

        std::vector<Record> recs;
        for (const auto& interval : intervals) {
            recs.push_back(Record(interval.start, Event::BGN));
            recs.push_back(Record(interval.end, Event::END));
        }

        std::sort(recs.begin(), recs.end(),
            [] (const auto& lhs, const auto& rhs) {
                if (lhs.time == rhs.time) {
                    return lhs.type < rhs.type;
                }
                return lhs.time < rhs.time;
            }
        );

        int count = 0;
        int ans = 0;

        for (const auto& rec : recs) {
            if (rec.type == Event::BGN) {
                ++count;
                ans = std::max(ans, count);
            } else {
                --count;
            }
        }

        return ans;
    }

private:
    enum Event {
        END,
        BGN
    };
};
```