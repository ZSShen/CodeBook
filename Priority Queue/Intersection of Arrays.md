
# Problem
### LintCode 793. Intersection of Arrays

https://www.lintcode.com/problem/intersection-of-arrays/description

# Solution
```c++


struct Record {
    int num;
    int id;
    int index;

    Record(int num, int id, int index)
      : num(num), id(id), index(index)
    { }
};


struct RecordCompare {
    bool operator() (const auto& lhs, const auto& rhs) {
        return lhs.num > rhs.num;
    }
};


class Solution {
public:
    /**
     * @param arrs: the arrays
     * @return: the number of the intersection of the arrays
     */
    int intersectionOfArrays(vector<vector<int>> &arrs) {
        // write your code here

        std::priority_queue<Record, std::vector<Record>, RecordCompare> queue;

        int k = arrs.size();
        for (int i = 0 ; i < k ; ++i) {
            if (!arrs[i].empty()) {
                std::sort(arrs[i].begin(), arrs[i].end());
                queue.push(Record(arrs[i][0], i, 0));
            }
        }

        // If all vectors are empty.
        if (queue.empty()) {
            return 0;
        }

        auto rec = queue.top();
        queue.pop();

        int prev = rec.num;
        int count = 1;
        int id = rec.id;
        int index = rec.index;

        if (index < arrs[id].size() - 1) {
            queue.push(Record(arrs[id][index + 1], id, index + 1));
        }

        int ans = 0;

        while (!queue.empty()) {
            rec = queue.top();
            queue.pop();

            int curr = rec.num;
            id = rec.id;
            index = rec.index;

            if (index < arrs[id].size() - 1) {
                queue.push(Record(arrs[id][index + 1], id, index + 1));
            }

            if (curr == prev) {
                ++count;
            }

            if (curr != prev) {
                if (count >= k) {
                    ++ans;
                }
                count = 1;
                prev = curr;
            }
        }

        if (count >= k) {
            ++ans;
        }

        return ans;
    }
};
```
