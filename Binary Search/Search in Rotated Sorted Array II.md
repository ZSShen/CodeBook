
# Problem
### LintCode 63. Search in Rotated Sorted Array II
https://www.lintcode.com/problem/search-in-rotated-sorted-array-ii/description

# Solution
```c++
class Solution {
public:
    /**
     * @param A: an integer ratated sorted array and duplicates are allowed
     * @param target: An integer
     * @return: a boolean
     */
    bool search(vector<int> &A, int target) {
        // write your code here

        int n = A.size();
        if (n == 0) {
            return false;
        }

        int l = 0, r = n - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;

            if (A[m] == target) {
                return true;
            }

            // The right portion is sorted.
            if (A[m] < A[r]) {
                if (A[m] < target && target < A[r]) {
                    l = m;
                } else {
                    r = m;
                }
            }
            // The left portion is sorted;
            else if (A[m] > A[r]) {
                if (A[l] < target && target < A[m]) {
                    r = m;
                } else {
                    l = m;
                }
            }
            // Implies A[m] == A[r] != target, and thus we can prune A[r].
            else {
                --r;
            }
        }

        return A[l] == target || A[r] == target;
    }
};
```