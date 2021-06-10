
# Problem
### LeetCode 973. K Closest Points to Origin
https://leetcode.com/problems/k-closest-points-to-origin

# Solution
```c++
struct Record {
    int x, y;
    double d;

    Record(int x, int y, double d)
        : x(x), y(y), d(d)
    { }
};


struct RecordCompare {
    bool operator() (const Record& lhs, const Record& rhs) {
        return lhs.d < rhs.d;
    }
};


class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {

        /**
         *  TC: O(N * logK)
         *  SC: O(K)
         */

        priority_queue<Record, vector<Record>, RecordCompare> q;

        for (const auto& p : points) {
            int x = p[0], y = p[1];
            double d = sqrt(x * x + y * y);

            q.push(Record(x, y, d));
            if (q.size() > k) {
                q.pop();
            }
        }

        vector<vector<int>> ans;
        while (!q.empty()) {
            auto r = q.top();
            q.pop();
            ans.push_back({r.x, r.y});
        }

        return ans;
    }
};
```