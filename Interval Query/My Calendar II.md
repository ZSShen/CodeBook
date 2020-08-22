
# Problem
### LeetCode 731. My Calendar II
https://leetcode.com/problems/my-calendar-ii/

# Solution
```c++
class MyCalendarTwo {
public:
    MyCalendarTwo() {

    }

    bool book(int s1, int e1) {

        /**
            (s1, e1), (s2, e2)
                |-----------|
                    |-----------|

                    |-----------|
                |-----------|

                    |---|
                |-----------|

                |-----------|
                    |---|

             max(s1, s2) < min(e1, e2)

                |-----|
                        |-----|
        */

        for (const auto& kv : overlaps) {
            int b = max(s1, kv.first);
            int e = min(e1, kv.second);
            if (b < e) {
                return false;
            }
        }

        for (const auto& kv : segments) {
            int b = max(s1, kv.first);
            int e = min(e1, kv.second);
            if (b < e) {
                overlaps.push_back({b, e});
            }
        }

        segments.push_back({s1, e1});
        return true;
    }

private:
    vector<pair<int, int>> segments;
    vector<pair<int, int>> overlaps;
};

/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * MyCalendarTwo* obj = new MyCalendarTwo();
 * bool param_1 = obj->book(start,end);
 */
```
