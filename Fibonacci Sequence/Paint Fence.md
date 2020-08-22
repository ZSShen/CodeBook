
# Problem
### LeetCode 276. Paint Fence
https://leetcode.com/problems/paint-fence/

# Solution
```c++
class Solution {
public:
    int numWays(int n, int k) {

        /**
            1st => k

            1st 2nd
            => diff color => k^2 - k
            => same color => k

            1st 2nd 3rd
            => make the 3rd one have different colors with the 2nd one
                (diff_color + same_color) * (k - 1)
            => make the 3rd one have the same color as the 2nd one
                diff_color * 1
        */

        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return k;
        }
        if (n == 2) {
            return k * k;
        }

        int diff_color = k * k - k;
        int same_color = k;

        for (int i = 3 ; i <= n ; ++i) {
            int prev_diff_color = diff_color;
            diff_color = (k - 1) * (diff_color + same_color);
            same_color = prev_diff_color;
        }

        return diff_color + same_color;
    }
};
```