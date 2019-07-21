
# Problem
### LintCode 81. Find Median from Data Stream
https://www.lintcode.com/problem/find-median-from-data-stream/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: the median of numbers
     */
    vector<int> medianII(vector<int> &nums) {
        // write your code here

        std::priority_queue<int, std::vector<int>, std::greater<int>> min;
        std::priority_queue<int, std::vector<int>, std::less<int>> max;

        std::vector<int> ans;
        for (int num : nums) {
            enQueue(min, max, num);
            reBalance(min, max);
            ans.push_back(getMedian(min, max));
        }

        return ans;
    }

private:
    void enQueue(auto& min, auto& max, int num) {

        if (max.empty()) {
            max.push(num);
            return;
        }

        if (num <= max.top()) {
            max.push(num);
        } else {
            min.push(num);
        }
    }

    void reBalance(auto& min, auto& max) {

        int max_size = max.size();
        int min_size = min.size();

        if (max_size > min_size + 1) {
            int num = max.top();
            max.pop();
            min.push(num);
        }

        if (min_size > max_size + 1) {
            int num = min.top();
            min.pop();
            max.push(num);
        }
    }

    int getMedian(auto& min, auto& max) {

        int max_size = max.size();
        int min_size = min.size();

        if (max_size > min_size) {
            return max.top();
        }

        if (min_size > max_size) {
            return min.top();
        }

        return max.top();
    }
};
```