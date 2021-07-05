
# Problem
### LeetCode 341. Flatten Nested List Iterator
https://leetcode.com/problems/flatten-nested-list-iterator

# Solution
```c++
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */

class NestedIterator {
public:
    NestedIterator(vector<NestedInteger> &list) {

        int n = list.size();
        for (int i = n - 1 ; i >= 0 ; --i) {
            stk.emplace(move(list[i]));
        }
    }

    int next() {
        int elem = stk.top().getInteger();
        stk.pop();
        return elem;
    }

    bool hasNext() {

        while (!stk.empty()) {
            if (stk.top().isInteger()) {
                return true;
            }

            auto list = stk.top().getList();
            stk.pop();

            int n = list.size();
            for (int i = n - 1 ; i >= 0 ; --i) {
                stk.emplace(move(list[i]));
            }
        }

        return false;
    }

private:
    stack<NestedInteger> stk;
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```