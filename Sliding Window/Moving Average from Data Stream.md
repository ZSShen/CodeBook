
# Problem
### LintCode 642. Moving Average from Data Stream
https://www.lintcode.com/problem/moving-average-from-data-stream/description

# Solution
```c++
class MovingAverage {
public:
    /*
    * @param size: An integer
    */MovingAverage(int size)
      : capacity(size), size(0), sum(0.0) {
        // do intialization if necessary
    }

    /*
     * @param val: An integer
     * @return:
     */
    double next(int val) {
        // write your code here

        if (size < capacity) {
            sum += val;
            deque.push_back(val);
            ++size;

            return sum / static_cast<double>(size);
        }

        sum -= deque.front();
        deque.pop_front();
        sum += val;
        deque.push_back(val);

        return sum / static_cast<double>(size);
    }

private:
    int capacity;
    int size;
    double sum;
    std::deque<double> deque;
};

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param = obj.next(val);
 */
```