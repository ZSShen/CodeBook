
# Problem
### LintCode 22. Flatten List
https://www.lintcode.com/problem/flatten-list

# Solution
```c++
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
class Solution {
public:
    // @param nestedList a list of NestedInteger
    // @return a list of integer
    vector<int> flatten(vector<NestedInteger> &list) {
        // Write your code here

        vector<int> ans;

        stack<NestedInteger> stk;
        int n = list.size();

        for (int i = n - 1 ; i >= 0 ; --i) {
            stk.emplace(move(list[i]));
        }

        while (!stk.empty()) {
            auto item = stk.top();
            stk.pop();

            if (item.isInteger()) {
                ans.emplace_back(item.getInteger());
            } else {
                auto& items = item.getList();
                n = items.size();

                for (int i = n - 1 ; i >= 0 ; --i) {
                    stk.emplace(move(items[i]));
                }
            }
        }

        return ans;
    }
};
```