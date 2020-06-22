
# Problem
### LintCode 1053. Previous Permutation With One Swap
https://leetcode.com/problems/previous-permutation-with-one-swap/

# Solution
```c++
class Solution {
public:
    vector<int> prevPermOpt1(vector<int>& A) {

        int n = A.size();
        int l = n - 2;
        while (l >= 0 && A[l + 1] >= A[l]) {
            --l;
        }

        // The smallest permutation.
        if (l == -1) {
            return A;
        }

        int r = 0;
        int num = -1;
        for (int i = n - 1 ; i > l ; --i) {
            if (A[i] >= num && A[i] < A[l]) {
                num = A[i];
                r = i;
            }
        }

        swap(A[l], A[r]);
        return A;
    }
};
```