
# Problem
### LeetCode 731. My Calendar II
https://leetcode.com/problems/my-calendar-ii/

# Solution
```c++
class MyCalendarTwo {
public:
    MyCalendarTwo() {

    }

    bool book(int start, int end) {

        /**
         *  TC: O(N^2), where
         *      N is the number of queries
         *
         *  SC: O(N)
         */

        ++delta[start];
        --delta[end];

        int count = 0;

        for (const auto& p : delta) {
            count += p.second;
            if (count > 2) {
                --delta[start];
                ++delta[end];
                return false;
            }
        }

        return true;
    }

private:
    map<int, int> delta;
};

/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * MyCalendarTwo* obj = new MyCalendarTwo();
 * bool param_1 = obj->book(start,end);
 */
```
