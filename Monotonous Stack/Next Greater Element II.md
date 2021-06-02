
# Problem
### LintCode 1201. Next Greater Element II
https://www.lintcode.com/problem/next-greater-element-ii/description

# Solution
```c++
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: (N)
         *
         *  Flatten the circular traversal by doubling the array size and
         *  checking each element twice.
         */

        int n = nums.size();
        int nn = n << 1;

        stack<int> stk;
        vector<int> ans(n, -1);

        for (int i = 0 ; i < nn ; ++i) {
            int j = i % n;
            int num = nums[j];

            while (!stk.empty() && num > nums[stk.top()]) {
                ans[stk.top()] = num;
                stk.pop();
            }

            stk.emplace(j);
        }

        return ans;
    }
};
```