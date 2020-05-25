
# Problem
### LeetCode 1411. Number of Ways to Paint N × 3 Grid
https://leetcode.com/problems/number-of-ways-to-paint-n-3-grid/

# Solution
```c++
class Solution {
public:
    int numOfWays(int n) {

        long c2 = 6;
        long c3 = 6;

        for (int i = 2 ; i <= n ; ++i) {
            long new_c2 = (3 * c2 + 2 * c3) % 1000000007;
            long new_c3 = (2 * c2 + 2 * c3) % 1000000007;
            c2 = new_c2;
            c3 = new_c3;
        }

        return (c2 + c3) % 1000000007;
    }
};
```