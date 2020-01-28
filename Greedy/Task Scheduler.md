
# Problem
### LintCode 945. Task Scheduler
https://www.lintcode.com/problem/task-scheduler/description

# Solution
```c++
class Solution {
public:
    /**
     * @param tasks: the given char array representing tasks CPU need to do
     * @param n: the non-negative cooling interval
     * @return: the least number of intervals the CPU will take to finish all the given tasks
     */
    int leastInterval(string &tasks, int n) {
        // write your code here

        unordered_map<char, int> map;
        for (char task : tasks) {
            ++map[task];
        }

        priority_queue<int, vector<int>, less<int>> queue;
        for (const auto& pair : map) {
            queue.emplace(pair.second);
        }

        int cycle = 0;
        while (!queue.empty()) {

            vector<int> temp;
            for (int i = 0 ; i < n + 1 ; ++i) {
                if (!queue.empty()) {
                    temp.emplace_back(queue.top());
                    queue.pop();
                }
            }

            for (int task : temp) {
                if (--task > 0) {
                    queue.emplace(task);
                }
            }

            cycle += queue.empty() ? temp.size() : n + 1;
        }

        return cycle;
    }
};
```