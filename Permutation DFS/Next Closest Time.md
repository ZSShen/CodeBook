
# Problem
### LintCode 862. Next Closest Time
https://www.lintcode.com/problem/next-closest-time/description

# Solution
```c++
class Solution {
public:
    /**
     * @param time: the given time
     * @return: the next closest time
     */
    string nextClosestTime(string &time) {
        // write your code here

        std::vector<int> pool;
        pool.push_back(time[0] - '0');
        pool.push_back(time[1] - '0');
        pool.push_back(time[3] - '0');
        pool.push_back(time[4] - '0');

        int timestamp =
            (pool[0] * 10 + pool[1]) * 60 + (pool[2] * 10 + pool[3]);

        std::vector<int> config;
        std::vector<int> opt(pool);
        int diff = INT_MAX;

        runBackTracking(pool, 0, 4, timestamp, diff, config, opt);

        std::stringstream stream;
        stream << opt[0] << opt[1] << ':' << opt[2] << opt[3];
        return stream.str();
    }

private:
    void runBackTracking(
            std::vector<int>& pool,
            int depth, int bound,
            int timestamp,
            int& diff,
            std::vector<int>& config,
            std::vector<int>& opt) {

        if (depth == bound) {
            int hour = config[0] * 10 + config[1];
            if (hour > 23) {
                return;
            }

            int minute = config[2] * 10 + config[3];
            if (minute > 59) {
                return;
            }

            int new_timestamp = hour * 60 + minute;
            if (new_timestamp > 1440) {
                return;
            }

            if (new_timestamp == timestamp) {
                return;
            }

            int new_diff;
            if (new_timestamp > timestamp) {
                new_diff = new_timestamp - timestamp;
            } else {
                new_diff = (1440 - timestamp) + new_timestamp;
            }

            if (new_diff < diff) {
                diff = new_diff;
                opt = config;
            }

            return;
        }

        for (int i = 0 ; i < bound ; ++i) {
            config.push_back(pool[i]);
            runBackTracking(
                pool, depth + 1, bound, timestamp, diff, config, opt);
            config.pop_back();
        }
    }
};
```