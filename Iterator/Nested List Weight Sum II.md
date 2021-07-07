
# Problem
### LeetCode 364. Nested List Weight Sum II
https://leetcode.com/problems/nested-list-weight-sum-ii

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
    int depthSumInverse(vector<NestedInteger>& list) {

        /**
         *  TC: O(N), where
         *      N is the number of objects
         *
         *  SC: O(N)
         */

        stack<pair<NestedInteger, int>> stk;
        int n = list.size();
        for (int i = n - 1 ; i >= 0 ; --i) {
            stk.push({list[i], 1});
        }

        vector<pair<int, int>> res;
        int max_depth = 0;

        while (!stk.empty()) {
            auto pair = stk.top();
            stk.pop();

            auto& item = pair.first;
            int depth = pair.second;
            max_depth = max(max_depth, depth);

            if (item.isInteger()) {
                res.push_back({item.getInteger(), depth});
            } else {
                auto nested = item.getList();
                n = nested.size();
                for (int i = n - 1 ; i >= 0 ; --i) {
                    stk.push({nested[i], depth + 1});
                }
            }
        }

        int ans = 0;
        for (auto& pair : res) {
            ans += pair.first * (max_depth - pair.second + 1);
        }
        return ans;
    }
};
```