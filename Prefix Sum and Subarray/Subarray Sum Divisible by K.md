
# Problem
### LeetCode 974. Subarray Sums Divisible by K
https://leetcode.com/problems/subarray-sums-divisible-by-k/

# Solution
```c++
class Solution {
public:
    int subarraysDivByK(vector<int>& A, int K) {

        /**
            A: 4, 5, 0, -2, -3, 1

            G[0]: 1
            G[1]: 0
            G[2]: 1
            G[3]: 0
            G[4]: 4

            Prefixes: 4, 9, 9, 7, 4, 5
            Count.  : 0, 1, 3, 3, 6, 7
        */

        vector<int> map(K, 0);
        map[0] = 1;

        int count = 0;
        int prefix = 0;

        for (int num : A) {
            prefix += num;
            int rem = prefix % K;
            if (rem < 0) {
                rem += K;
            }
            count += map[rem];
            ++map[rem];
        }

        return count;
    }
};
```
