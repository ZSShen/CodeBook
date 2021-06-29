
# Problem
### LintCode 945. Task Scheduler
https://www.lintcode.com/problem/task-scheduler/description

# Solution
```c++
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {

        /**
         *  TC: O(N), where
         *      N is the number of tasks
         *
         *  SC: O(26)
         *
         *  A: 5
         *  B: 4
         *  C: 2
         *
         *  n = 2
         *
         *  A _ _ A _ _ A _ _ A _ _ A
         *
         *  A B _ A B _ A B _ A B _ A
         *
         *  A B C A B C A B _ A B _ A
         *
         *  # of tasks      : 11
         *  # of idle slots : 2
         */

        vector<int> freq(26);
        for (char ch : tasks) {
            ++freq[ch - 'A'];
        }

        sort(freq.begin(), freq.end());

        int f_max = freq[25];
        int idle_slots = (f_max - 1) * n;
        for (int i = 24 ; i >= 0 && freq[i] > 0 && idle_slots > 0 ; --i) {
            idle_slots -= min(f_max - 1, freq[i]);
        }

        return (idle_slots > 0) ? tasks.size() + idle_slots : tasks.size();
    }
};
```