
# Problem
### LeetCode 7. Reverse Integer
https://leetcode.com/problems/reverse-integer

# Solution
```c++
class Solution {
public:
    int reverse(int x) {

        /**
         *  TC: O(log(x)), with base 10
         *  SC: O(1)
         */

        int ans = 0;

        while (x != 0) {
            int test = ans * 10 + (x % 10);
            // Check for potential integer overflow.
            if (test / 10 != ans) {
                return 0;
            }
            ans = test;
            x /= 10;
        }

        return ans;
    }
};
```