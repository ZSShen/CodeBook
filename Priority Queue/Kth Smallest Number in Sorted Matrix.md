
# Problem
### LeetCode 378. Kth Smallest Element in a Sorted Matrix
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix

# Solution
```c++
struct Record {
    int num;
    int r;
    int c;

    Record(int num, int r, int c)
      : num(num),
        r(r),
        c(c)
    { }
};


struct RecordCompare {
    bool operator() (const Record& lhs, const Record& rhs) {
        return lhs.num > rhs.num;
    }
};


class Solution {
public:
    int kthSmallest(vector<vector<int>>& mat, int k) {

        /**
         *  TC: O(KlogK)
         *
         *  SC: O(K)
         *      We have up to K elements stored in the minimum heap
         */

        int m = mat.size();
        int n = mat[0].size();

        priority_queue<Record, vector<Record>, RecordCompare> q;
        q.emplace(mat[0][0], 0, 0);

        unordered_set<int> visit;
        visit.emplace(0);

        int num;
        for (int i = 0 ; i < k ; ++i) {
            auto record = q.top();
            q.pop();

            num = record.num;
            int r = record.r;
            int c = record.c;

            int code = r * n + (c + 1);
            if (c + 1 < n && visit.count(code) == 0) {
                q.emplace(mat[r][c + 1], r, c + 1);
                visit.emplace(code);
            }

            // Check the below neighbor.
            code = (r + 1) * n + c;
            if (r + 1 < m && visit.count(code) == 0) {
                q.emplace(mat[r + 1][c], r + 1, c);
                visit.emplace(code);
            }
        }

        return num;
    }
};
```