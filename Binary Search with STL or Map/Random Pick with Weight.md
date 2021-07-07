
# Problem
### LeetCode 528. Random Pick with Weight
https://leetcode.com/problems/random-pick-with-weight/

# Solution
```c++
class Solution {
public:
    Solution(vector<int>& w) {

        /**
         *  TC: O(logN), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *
         *    Input     : 3, 4, 1, 2
         *    Prefix Sum: 3, 7, 8, 10
         *
         *    1st element: [0, 2]
         *    2nd        : [3, 6]
         *    3rd        : [7, 7]
         *    4th        : [8, 10]
         */

        sum.emplace_back(w[0]);

        int n = w.size();
        for (int i = 1 ; i < n ; ++i) {
            sum.emplace_back(sum.back() + w[i]);
        }
    }

    int pickIndex() {

        int x = rand() % sum.back();
        return upper_bound(sum.begin(), sum.end(), x) - sum.begin();
    }

private:
    vector<int> sum;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(w);
 * int param_1 = obj->pickIndex();
 */
```
