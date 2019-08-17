
# Problem
### LintCode 460. Find K Closest Elements
https://www.lintcode.com/problem/find-k-closest-elements/description

# Solution
```c++
class Solution {
public:
    /**
     * @param A: an integer array
     * @param target: An integer
     * @param k: An integer
     * @return: an integer array
     */
    vector<int> kClosestNumbers(vector<int> &A, int target, int k) {
        // write your code here

        int n = A.size();
        if (n == 0 || k == 0) {
            return {};
        }

        int l = 0, r = n - 1;
        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (A[m] < target) {
                l = m;
            } else {
                r = m;
            }
        }

        int closest = A[l];
        int pivot = l;
        if (std::abs(A[r] - target) < std::abs(A[l] - target)) {
            closest = A[r];
            pivot = r;
        }

        std::vector<int> ans;
        ans.push_back(closest);

        l = pivot - 1;
        r = pivot + 1;
        for (int i = 0 ; i < k - 1 ; ++i) {
            if (l >= 0 && r < n) {
                if (std::abs(target - A[l]) <= std::abs(A[r] - target)) {
                    ans.push_back(A[l--]);
                } else {
                    ans.push_back(A[r++]);
                }
            } else {
                if (l < 0) {
                    ans.push_back(A[r++]);
                } else if (r >= n) {
                    ans.push_back(A[l--]);
                }
            }
        }

        return ans;
    }
};
```