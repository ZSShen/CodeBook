
# Problem
### LeetCode 1539. Kth Missing Positive Number
https://leetcode.com/problems/kth-missing-positive-number

# Solution
```c++
class Solution {
public:
    int findKthPositive(vector<int>& arr, int k) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         *
         *  Find the minimum index i,
         *      such that arr[i] - i - 1 >= k
         */

        int n = arr.size();
        int l = 0, r = n - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (arr[m] - m - 1 >= k) {
                r = m;
            } else {
                l = m;
            }
        }

        if (arr[l] - l - 1 >= k) {
            return l + k;
        }
        if (arr[r] - r - 1 >= k) {
            return r + k;
        }

        // There is no missing element in the input array.
        return n + k;
    }
};
```