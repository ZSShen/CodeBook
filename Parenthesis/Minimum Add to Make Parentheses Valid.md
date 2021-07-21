
# Problem
### LeetCode 921. Minimum Add to Make Parentheses Valid
https://leetcode.com/problems/minimum-add-to-make-parentheses-valid

# Solution
```c++
class Solution {
public:
    int minAddToMakeValid(string S) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(1)
         *
            Maintain a counter to balance parentheses

            ( )  )  ) ( (
            1 0 -1 -2 1 2  => |-2| + |2| = 4

            ( ( (
            1 2 3          => |3| = 3

            ) ( )  )
           -1 1 0 -1       => |-1| + |-1| = 2
        */

        int count = 0, ans = 0;

        for (char ch : S) {
            if (ch == ')') {
                --count;
            } else {
                if (count < 0) {
                    ans += -count;
                    count = 0;
                }
                ++count;
            }
        }

        ans += abs(count);
        return ans;
    }
};
```