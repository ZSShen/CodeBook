
# Problem
### LeetCode 716. Max Stack
https://leetcode.com/problems/max-stack

# Solution
```c++
class MaxStack {
public:
    /** initialize your data structure here. */
    MaxStack() {
        /**
         *  TC: O(1)    , for read operators
         *      O(NlogN), for write operators, where
         *      N is the number of elements
         *
         *  SC: O(N)
         */
    }

    void push(int x) {
        elems.push_front(x);
        auto it = elems.begin();
        map[x].push_back(it);
    }

    int pop() {
        int x = elems.front();
        elems.pop_front();

        map[x].pop_back();
        if (map[x].empty()) {
            map.erase(x);
        }

        return x;
    }

    int top() {
        return elems.front();
    }

    int peekMax() {
        return map.rbegin()->first;
    }

    int popMax() {
        int x = map.rbegin()->first;

        auto it = map[x].back();
        map[x].pop_back();
        if (map[x].empty()) {
            map.erase(x);
        }

        elems.erase(it);
        return x;
    }

private:
    list<int> elems;
    map<int, vector<list<int>::iterator>> map;
};

/**
 * Your MaxStack object will be instantiated and called as such:
 * MaxStack* obj = new MaxStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->peekMax();
 * int param_5 = obj->popMax();
 */
```