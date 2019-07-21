
# Problem
### LintCode 12. Min Stack
https://www.lintcode.com/problem/min-stack/description

# Solution
```c++
class MinStack {
public:
    MinStack() {
        // do intialization if necessary
    }

    /*
     * @param number: An integer
     * @return: nothing
     */
    void push(int number) {
        // write your code here

        if (stk.empty()) {
            min_stk.push(number);
        } else {
            min_stk.push(std::min(number, min_stk.top()));
        }

        stk.push(number);
    }

    /*
     * @return: An integer
     */
    int pop() {
        // write your code here

        int num = stk.top();

        stk.pop();
        min_stk.pop();

        return num;
    }

    /*
     * @return: An integer
     */
    int min() {
        // write your code here

        return min_stk.top();
    }

private:
    std::stack<int> stk;
    std::stack<int> min_stk;
};
```