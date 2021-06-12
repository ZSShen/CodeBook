
# Problem
### LeetCode 480. Sliding Window Median
https://leetcode.com/problems/sliding-window-median

# Solution
```c++
class Solution {
public:
    vector<double> medianSlidingWindow(vector<int>& nums, int k) {

        /**
         *  TC: O(NlogK), where
         *      N is the number of elements
         *      K is the window size
         *
         *  SC: O(K)
         */

        multiset<int, greater<int>> max_q;
        multiset<int, less<int>> min_q;
        vector<double> ans;

        int n = nums.size(), c = 0;
        for (int i = 0 ; i < n ; ++i) {
            insert(nums[i], max_q, min_q);
            ++c;

            if (c > k) {
                remove(nums[i - k], max_q, min_q);
                --c;
            }

            rebalance(max_q, min_q);

            if (c == k) {
                ans.emplace_back(query(max_q, min_q));
            }
        }

        return ans;
    }

private:
    void insert(
            int num,
            multiset<int, greater<int>>& max_q,
            multiset<int, less<int>>& min_q) {

        if (max_q.empty()) {
            max_q.emplace(num);
            return;
        }

        if (num <= *max_q.begin()) {
            max_q.emplace(num);
        } else {
            min_q.emplace(num);
        }
    }

    void rebalance(
            multiset<int, greater<int>>& max_q,
            multiset<int, less<int>>& min_q) {

        int M_size = max_q.size();
        int m_size = min_q.size();

        if (M_size - m_size > 1) {
            auto it = max_q.begin();
            min_q.emplace(*it);
            max_q.erase(it);
            return;
        }

        if (m_size - M_size > 1) {
            auto it = min_q.begin();
            max_q.emplace(*it);
            min_q.erase(it);
        }
    }

    void remove(
            int num,
            multiset<int, greater<int>>& max_q,
            multiset<int, less<int>>& min_q) {

        auto it = max_q.find(num);
        if (it != max_q.end()) {
            max_q.erase(it);
            return;
        }

        it = min_q.find(num);
        min_q.erase(it);
    }

    double query(
            multiset<int, greater<int>>& max_q,
            multiset<int, less<int>>& min_q) {

        int M_size = max_q.size();
        int m_size = min_q.size();

        if (M_size == m_size) {
            double a = *max_q.begin();
            double b = *min_q.begin();
            return (a + b) / 2;
        }

        return M_size > m_size ? *max_q.begin() : *min_q.begin();
    }
};
```