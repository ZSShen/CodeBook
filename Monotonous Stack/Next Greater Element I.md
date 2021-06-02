
# Problem
### LeetCode 496. Next Greater Element I
https://leetcode.com/problems/next-greater-element-i

# Solution
```c++
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {

        /**
         *  TC: O(N), where
         *      N is the number of elements of nums2
         *
         *  SC: O(N)
         *
         *  Maintain a monotonous non-increasing stack for the elements of nums2
         *
         *  nums2:  1 3 4 2
         *
         *  stk:
         *  next[1] = -1, next[3] = -1, next[4] = -1, next[2] = -1
         *
         *  stk: 1
         *  next[1] = -1, next[3] = -1, next[4] = -1, next[2] = -1
         *
         *  stk: 3
         *  next[1] = 3 , next[3] = -1, next[4] = -1, next[2] = -1
         *
         *  stk: 4
         *  next[1] = 3 , next[3] = 4, next[4] = -1, next[2] = -1
         *
         *  stk: 4 2
         *  next[1] = 3 , next[3] = 4, next[4] = -1, next[2] = -1
         *
         *
         *  Then, map the next greater elements for the elements of nums1
         */

        unordered_map<int, int> map;
        stack<int> stk;

        for (int num : nums2) {
            while (!stk.empty() && num > stk.top()) {
                map[stk.top()] = num;
                stk.pop();
            }
            stk.emplace(num);
        }

        vector<int> ans;
        for (int num : nums1) {
            int next = (map.count(num) == 1) ? map[num] : -1;
            ans.emplace_back(next);
        }

        return ans;
    }
};
```