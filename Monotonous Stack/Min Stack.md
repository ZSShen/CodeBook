
# Problem
### LeetCode 155. Min Stack
https://leetcode.com/problems/min-stack

# Solution
```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack()
        : size(0) {

    }

    void push(int x) {

        stk.emplace_back(x);

        if (size == 0) {
            dp.emplace_back(x);
        } else {
            dp.emplace_back(min(x, dp.back()));
        }

        ++size;
    }

    void pop() {
        stk.pop_back();
        dp.pop_back();
        --size;
    }

    int top() {
        return stk.back();
    }

    int getMin() {
        return dp.back();
    }

private:
    int size;
    vector<int> stk;
    vector<int> dp;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```