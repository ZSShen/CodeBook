
# Problem
### LeetCode 1005. Maximize Sum Of Array After K Negations
https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/

# Solution
```c++
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& A, int K) {

        sort(A.begin(), A.end());

        int n = A.size();
        for (int i = 0 ; i < n ; ++i) {
            if (A[i] >= 0) {
                break;
            }

            A[i] = -A[i];
            --K;
            if (K == 0) {
                break;
            }
        }

        int sum = accumulate(A.begin(), A.end(), 0);
        if (K % 2 == 1) {
            sum -= *min_element(A.begin(), A.end()) * 2;
        }
        return sum;
    }
};
```
