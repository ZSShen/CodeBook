
# Problem
### LeetCode 135. Candy
https://leetcode.com/problems/candy/

# Solution
```c++
class Solution {
public:
    int candy(vector<int>& ratings) {

        /*
            L, C, R  rate(L) >= rate(C) && rate(R) >= rate(C)  => 1
                     rate(L) < rate(C) && rate(R) < rate(C)  => max(cand[L], cand[R]) + 1
                     rate(L) >= rate(C) && rate(R) < rate(C) => max(1, cand[R] + 1)
                     rate(L) < rate(C) && rate(R) >= rate(C) => max(cand[L] + 1, 1)

             0, 1, 2
            [1, 2, 2]  => (0, 1), (1, 2), (2, 2)
                           1       2       1

             0, 1, 2
            [1, 0, 2]  => (1, 0), (0, 1), (2, 2)
                           1       2       2

        int n = ratings.size();
        vector<int> candies(n, 0);

        // (first, second) => (id, rate)
        vector<pair<int, int>> children;
        for (int i = 0 ; i < n ; ++i) {
            children.emplace_back(i, ratings[i]);
        }

        sort(children.begin(), children.end(),
            [](const auto& lhs, const auto& rhs) {
                return lhs.second < rhs.second;
            });

        int ans = 0;
        for (int i = 0 ; i < n ; ++i) {
            int id = children[i].first;

            int c_rate = children[i].second;
            int l_rate = (id > 0) ? ratings[id - 1] : -1;
            int r_rate = (id < n - 1) ? ratings[id + 1] : -1;

            // 1st
            if (l_rate >= c_rate && r_rate >= c_rate) {
                candies[id] = 1;
            }
            // 2nd
            else if (l_rate < c_rate && r_rate < c_rate) {
                int l_candy = (id > 0) ? candies[id - 1] : 0;
                int r_candy = (id < n - 1) ? candies[id + 1] : 0;
                candies[id] = max(l_candy, r_candy) + 1;
            }
            // 3rd
            else if (l_rate >= c_rate && r_rate < c_rate) {
                int r_candy = (id < n - 1) ? candies[id + 1] : 0;
                candies[id] = max(1, r_candy + 1);
            }
            // 4th
            else if (l_rate < c_rate && r_rate >= c_rate) {
                int l_candy = (id > 0) ? candies[id - 1] : 0;
                candies[id] = max(l_candy + 1, 1);
            }

            ans += candies[id];
        }

        return ans;
        */

        int n = ratings.size();

        vector<int> l2r(n, 1);
        for (int i = 1 ; i < n ; ++i) {
            l2r[i] = (ratings[i - 1] < ratings[i]) ? l2r[i - 1] + 1 : 1;
        }

        vector<int> r2l(n, 1);
        for (int i = n - 2 ; i >= 0 ; --i) {
            r2l[i] = (ratings[i + 1] < ratings[i]) ? r2l[i + 1] + 1 : 1;
        }

        int ans = 0;
        for (int i = 0 ; i < n ; ++i) {
            ans += max(l2r[i], r2l[i]);
        }
        return ans;
    }
};
```
