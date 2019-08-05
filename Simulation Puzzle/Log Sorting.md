
# Problem
### LintCode 1380. Log Sorting
https://www.lintcode.com/problem/log-sorting/description

# Solution
```c++

struct Record {
    bool is_num;
    int serial;
    std::string id;
    std::string content;

    Record(bool is_num, int serial,
        const std::string& id, const std::string& content)
      : is_num(is_num), serial(serial), id(id), content(content)
    { }
};


class Solution {
public:
    /**
     * @param logs: the logs
     * @return: the log after sorting
     */
    vector<string> logSort(vector<string> &logs) {
        // Write your code here

        int n = logs.size();
        std::vector<Record> records;

        for (int i = 0 ; i < n ; ++i) {
            const auto& line = logs[i];

            auto pos = line.find(' ');
            auto id = line.substr(0, pos);
            ++pos;
            auto content = line.substr(pos, line.length() - pos);
            bool is_num = ('0' <= content[0] && content[0] <= '9');

            records.push_back(Record(is_num, i, id, content));
        }

        std::sort(records.begin(), records.end(),
            [](const auto& lhs, const auto& rhs) {

                // For rule #1.
                if (lhs.is_num != rhs.is_num) {
                    return !lhs.is_num;
                }

                // For rule #3.
                if (lhs.is_num == rhs.is_num && lhs.is_num == true) {
                    return lhs.serial < rhs.serial;
                }

                // For rule #2.
                int order = lhs.content.compare(rhs.content);
                if (order == 0) {
                    return lhs.id < rhs.id;
                }
                return order < 0;
            }
        );

        std::vector<std::string> ans;

        for (const auto& rec : records) {
            ans.push_back(rec.id + " " + rec.content);
        }

        return ans;
    }
};
```
