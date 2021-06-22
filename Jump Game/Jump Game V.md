
# Problem
### LeetCode 1340. Jump Game V
https://leetcode.com/problems/jump-game-v/

# Solution
```c++
class Solution {
public:
    int maxJumps(vector<int>& arr, int d) {

        /**
         *  TC: O(N * D), where
         *      N is the number of bars
         *      D is the given range
         *
         *  SC: O(N)
         */

        int n = arr.size();
        vector<int> dp(n);

        int ans = 1;
        for (int i = 0 ; i < n ; ++i) {
            ans = max(ans, topDown(arr, i, n, d, arr[i], dp));
        }
        return ans;
    }

private:
    int topDown(
            const vector<int>& arr,
            int bgn, int n, int d, int h,
            vector<int>& dp) {

        if (dp[bgn] > 0) {
            return dp[bgn];
        }

        int opt = 1;

        // Check the left neighbors.
        int end = max(bgn - d, 0);
        for (int i = bgn - 1 ; i >= end ; --i) {
            if (arr[i] >= h) {
                break;
            }
            opt = max(opt, 1 + topDown(arr, i, n, d, arr[i], dp));
        }

        end = min(bgn + d, n - 1);
        for (int i = bgn + 1 ; i <= end ; ++i) {
            if (arr[i] >= h) {
                break;
            }
            opt = max(opt, 1 + topDown(arr, i, n, d, arr[i], dp));
        }

        return dp[bgn] = opt;
    }
};
```