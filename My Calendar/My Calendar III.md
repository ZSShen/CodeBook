
# Problem
### LeetCode 732. My Calendar III
https://leetcode.com/problems/my-calendar-iii

# Solution
```c++
class MyCalendarThree {
public:
    MyCalendarThree() {

    }

    int book(int start, int end) {

        /**
         *  TC: O(N^2), where
         *      N is the number of queries
         *
         *  SC: O(N)
         */

        ++delta[start];
        --delta[end];

        int count = 0;
        int ans = 0;

        for (const auto& p : delta) {
            count += p.second;
            ans = max(ans, count);
        }

        return ans;
    }

private:
    map<int, int> delta;
};

/**
 * Your MyCalendarThree object will be instantiated and called as such:
 * MyCalendarThree* obj = new MyCalendarThree();
 * int param_1 = obj->book(start,end);
 */
```