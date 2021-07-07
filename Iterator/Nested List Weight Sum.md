
# Problem
### LeetCode 339. Nested List Weight Sum
https://leetcode.com/problems/nested-list-weight-sum

# Solution
```c++
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Constructor initializes an empty nested list.
 *     NestedInteger();
 *
 *     // Constructor initializes a single integer.
 *     NestedInteger(int value);
 *
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Set this NestedInteger to hold a single integer.
 *     void setInteger(int value);
 *
 *     // Set this NestedInteger to hold a nested list and adds a nested integer to it.
 *     void add(const NestedInteger &ni);
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
class Solution {
public:
    int depthSum(vector<NestedInteger>& list) {

        /**
         *  TC: O(N), where
         *      N is the number of objects
         *
         *  SC: O(N)
         */

        int ans = 0;

        stack<pair<NestedInteger, int>> stk;
        int n = list.size();
        for (int i = n - 1 ; i >= 0 ; --i) {
            stk.push({list[i], 1});
        }

        while (!stk.empty()) {
            auto rec = stk.top();
            stk.pop();

            auto& item = rec.first;
            int depth = rec.second;

            if (item.isInteger()) {
                ans += item.getInteger() * depth;
            } else {
                auto& nested = item.getList();
                n = nested.size();
                for (int i = n - 1 ; i >= 0 ; --i) {
                    stk.push({nested[i], depth + 1});
                }
            }
        }

        return ans;
    }
};
```