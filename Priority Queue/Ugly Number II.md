
# Problem
### LeetCode 264. Ugly Number II
https://leetcode.com/problems/ugly-number-ii

# Solution
```c++
class Solution {
public:
    int nthUglyNumber(int n) {

        /**
         * TC: O(NlogN)
         * SC: O(N)
         */

        set<long> set;
        set.emplace(1);
        long ans = 1;

        for (int i = 0 ; i < n ; ++i) {
            auto it = set.begin();
            ans = *it;
            set.erase(it);

            set.emplace(ans * 2);
            set.emplace(ans * 3);
            set.emplace(ans * 5);
        }

        return ans;
    }
};
```