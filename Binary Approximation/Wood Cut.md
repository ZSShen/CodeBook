
# Problem
### LintCode 183. Wood Cut
https://www.lintcode.com/problem/wood-cut/description

# Solution
```c++
class Solution {
public:
    /**
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    int woodCut(vector<int> &L, int k) {
        // write your code here

        /**
         *  n pieces of woods
         *
         *  s: The length of small pieces
         *  L1/s + L2/s + ... + Ln/s = ?
         *
         *  We need to find a s so that the above fuction is equal to k.
         *  Besides, s should be maximal.
         *
         *  For this, we can use binary approximation to gradually approach
         *  the ideal s:
         *      l = 1, r = Lmax
         *      s = (l + r) / 2
         *
         *  O(nlogL)
         */

        if (L.empty() || k == 0) {
            return 0;
        }

        int l = 1;
        int r = 0;
        for (int len : L) {
            if (len > r) {
                r = len;
            }
        }

        while (l + 1 < r) {
            int m = l + (r - l) / 2;

            if (countSmallPieces(L, m) >= k) {
                l = m;
            } else {
                r = m;
            }
        }

        if (countSmallPieces(L, l) < k) {
            return 0;
        }
        if (countSmallPieces(L, r) == k) {
            return r;
        } else {
            return l;
        }
    }

private:
    int countSmallPieces(const std::vector<int>& L, int s) {

        int count = 0;
        for (int len : L) {
            count += len / s;
        }

        return count;
    }
};
```