
# Problem
### LeetCode 346. Moving Average from Data Stream
https://leetcode.com/problems/moving-average-from-data-stream

# Solution
```c++
class MovingAverage {
public:
    /** Initialize your data structure here. */
    MovingAverage(int size)
        : capacity(size), size(0), sum(0)
    { }

    double next(int val) {
        sum += val;
        q.emplace_back(val);
        ++size;

        if (size > capacity) {
            sum -= q.front();
            q.pop_front();
            --size;
        }

        return static_cast<double>(sum) / size;
    }

private:
    int capacity, size, sum;
    deque<int> q;
};

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage* obj = new MovingAverage(size);
 * double param_1 = obj->next(val);
 */
```