
# Problem
### LeetCode 313. Super Ugly Number
https://leetcode.com/problems/super-ugly-number

# Solution
```c++
class Solution {
public:
    int nthSuperUglyNumber(int n, vector<int>& primes) {

        /**
         *  TC: O(N * logN * K), where
         *      K is the number of primes
         *
         *  SC: O(N * K)
         */

        set<int> set;
        set.emplace(1);

        int ans;
        for (int i = 0 ; i < n ; ++i) {
            auto it = set.begin();
            ans = *it;
            set.erase(it);

            for (int p : primes) {
                if (INT_MAX / p < ans) {
                    continue;
                }
                set.emplace(p * ans);
            }
        }

        return ans;
    }
};
```
