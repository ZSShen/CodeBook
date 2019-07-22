
# Problem
### LintCode 362. Sliding Window Maximum
https://www.lintcode.com/problem/sliding-window-maximum/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: A list of integers.
     * @param k: An integer
     * @return: The maximum number inside the window at each moving.
     */
    vector<int> maxSlidingWindow(vector<int> &nums, int k) {
        // write your code here

        /**
         *          1, 2, 7, 7, 8
         *
         *  Deque: 1
         *         1, 2
         *         2
         *         2, 7
         *         7    <= 1st step
         *
         *              <= Runtime Start
         *
         *         7, 7 <= 2nd step
         *         7
         *         7, 8 <= 3rd step
         *         8
         */

        int n = nums.size();
        if (n == 0 || k == 0) {
            return {};
        }

        std::deque<int> deque;
        std::vector<int> ans;

        for (int i = 0 ; i < k ; ++i) {
            enQueue(deque, i, nums);
        }
        ans.push_back(nums[deque.front()]);

        for (int i = k ; i < n ; ++i) {
            deQueue(deque, i - k);
            enQueue(deque, i, nums);
            ans.push_back(nums[deque.front()]);
        }

        return ans;
    }

private:
    void enQueue(auto& deque, int index, const auto& nums) {

        while (!deque.empty() && nums[index] >= nums[deque.back()]) {
            deque.pop_back();
        }
        deque.push_back(index);
    }

    void deQueue(auto& deque, int index) {

        if (deque.front() == index) {
            deque.pop_front();
        }
    }
};
```