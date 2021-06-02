
# Problem
### LeetCode 739. Daily Temperatures
https://leetcode.com/problems/daily-temperatures

# Solution
```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {

        int n = T.size();
        vector<int> ans(n);

        stack<int> stk;
        for (int i = 0 ; i < n ; ++i) {
            while (!stk.empty() && T[i] > T[stk.top()]) {
                ans[stk.top()] = i - stk.top();
                stk.pop();
            }
            stk.push(i);
        }

        return ans;
    }
};
```