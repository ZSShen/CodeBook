
# Problem
### LeetCode 975. Odd Even Jump
https://leetcode.com/problems/odd-even-jump/

# Solution
```c++
class Solution {
public:
    int oddEvenJumps(vector<int>& A) {

        int n = A.size();

        vector<bool> odds(n, false);
        vector<bool> evens(n, false);
        odds[n - 1] = true;
        evens[n - 1] = true;

        map<int, int> map;
        map[A[n - 1]] = n - 1;
        int ans = 1;

        for (int i = n - 2 ; i >= 0 ; --i) {
            int num = A[i];

            // Plan to apply a up jump from this position.
            auto it = map.lower_bound(num);
            if (it != map.end()) {
                odds[i] = evens[it->second];
            }

            // Plan to apply a down jump from this position.
            it = map.upper_bound(num);
            if (it != map.begin()) {
                evens[i] = odds[(--it)->second];
            }

            if (odds[i]) {
                ++ans;
            }
            map[num] = i;
        }

        return ans;
    }
};
```
