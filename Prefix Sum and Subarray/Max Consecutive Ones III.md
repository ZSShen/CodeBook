
# Problem
### Leetcode 1004. Max Consecutive Ones III
https://leetcode.com/problems/max-consecutive-ones-iii/

# Solution
```c++
class Solution {
public:
    int longestOnes(vector<int>& A, int K) {

        /**
         * Since all the elements in the array are either 1s or 0s,
         * we can transform the problem into finding the longest subarray
         * that fits the following equation:
         *
         * (j - i + 1) - SUM(i, j) <= K
         *
         * Given a subarray starting from i and ending at j.
         * SUM(i, j) means the sum of consecutive elements from the ith to the jth.
         * (j - i + 1) means the size of the subarray.
         *
         * We can use 2 pointers to maintain a sliding window and scan through
         * the array to check all the subarrays fulfilling the above equation.
         * Among all the subarrays, we pick the longest one.
         */

        int n = A.size();
        int ans = 0, sum = 0, l = 0;

        for (int r = 0 ; r < n ; ++r) {
            sum += A[r];

            // We have more than K 0s in the window, adjusting the window.
            while (l <= r && (r - l + 1) - sum > K) {
                sum -= A[l++];
            }

            ans = max(ans, r - l + 1);
        }

        return ans;
    }
};
```