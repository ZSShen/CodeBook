
# Problem
### LintCode 61. Search for a Range
https://www.lintcode.com/problem/search-for-a-range/description

# Solution
```c++
class Solution {
public:
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    vector<int> searchRange(vector<int> &A, int target) {
        // write your code here

        int n = A.size();
        if (n == 0) {
            return {-1, -1};
        }

        // Find the starting position.
        int l = 0, r = n - 1;
        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (target <= A[m]) {
                r = m;
            } else {
                l = m;
            }
        }

        int bgn = -1;
        if (A[l] == target) {
            bgn = l;
        } else if (A[r] == target) {
            bgn = r;
        }

        if (bgn == -1) {
            return {-1, -1};
        }

        // Find the ending position.
        l = 0, r = n - 1;
        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (target >= A[m]) {
                l = m;
            } else {
                r = m;
            }
        }

        int end = (A[r] == target) ? r : l;

        return {bgn, end};
    }
};
```