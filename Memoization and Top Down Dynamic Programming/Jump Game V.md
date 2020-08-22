
# Problem
### LeetCode 1340. Jump Game V
https://leetcode.com/problems/jump-game-v/

# Solution
```c++
class Solution {
public:
    int maxJumps(vector<int>& arr, int d) {

        int n = arr.size();
        int opt = 0;

        vector<int> memo(n, -1);

        for (int i = 0 ; i < n ; ++i) {
            topDown(i, n, d, arr, arr[i], opt, memo);
        }

        return opt;
    }

private:
    int topDown(
            int i, int n, int d,
            vector<int>& arr,
            int h,
            int& opt,
            vector<int>& memo) {

        // For memoization.
        if (memo[i] != -1) {
            return memo[i];
        }

        int local = 0;

        // Enumerate the first d combinations.
        int lo = max(0, i - d);
        for (int j = i - 1 ; j >= lo && arr[j] < arr[i] ; --j) {
            local = max(local, topDown(j, n, d, arr, arr[j], opt, memo));
        }

        // Enumerate the second d combinations.
        int hi = min(i + d, n - 1);
        for (int j = i + 1 ; j <= hi && arr[j] < arr[i] ; ++j) {
            local = max(local, topDown(j, n, d, arr, arr[j], opt, memo));
        }

        opt = max(opt, local + 1);
        return memo[i] = local + 1;
    }
};
```