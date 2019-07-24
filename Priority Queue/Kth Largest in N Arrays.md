
# Problem
### LintCode 543. Kth Largest in N Arrays
https://www.lintcode.com/problem/kth-largest-in-n-arrays/description

# Solution
```c++

class Solution {
public:
    /**
     * @param arrays: a list of array
     * @param k: An integer
     * @return: an integer, K-th largest element in N arrays
     */
    int KthInArrays(vector<vector<int>> &arrays, int k) {
        // write your code here

        std::priority_queue<int, std::vector<int>, std::greater<int>> queue;
        for (const auto& array : arrays) {
            for (int num : array) {
                queue.push(num);

                if (queue.size() > k) {
                    queue.pop();
                }
            }
        }

        return queue.top();
    }
};

```