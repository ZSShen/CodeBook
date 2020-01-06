
# Problem
### LintCode 1041. Reorganize String
https://www.lintcode.com/problem/reorganize-string/description?

# Solution
```c++

struct Record {
    char ch;
    int freq;

    Record(char ch, int freq)
        : ch(ch), freq(freq)
    { }
};

struct RecordCompare {
    bool operator() (const auto& lhs, const auto& rhs) {
        return lhs.freq < rhs.freq;
    }
};


class Solution {
public:
    string reorganizeString(string &S) {

        unordered_map<char, int> map;
        for (char ch : S) {
            ++map[ch];
        }

        priority_queue<Record, vector<Record>, RecordCompare> queue;
        for (const auto& pair : map) {
            queue.emplace(pair.first, pair.second);
        }

        string res;

        while (!queue.empty()) {
            auto fst = queue.top();
            queue.pop();

            if (queue.empty()) {
                if (fst.freq > 1) {
                    return "";
                }
                res.push_back(fst.ch);
                return res;
            }

            auto snd = queue.top();
            queue.pop();

            if (fst.ch != res.back()) {
                res.push_back(fst.ch);
                res.push_back(snd.ch);
            } else {
                res.push_back(snd.ch);
                res.push_back(fst.ch);
            }
            --fst.freq;
            --snd.freq;

            if (fst.freq > 0) {
                queue.emplace(std::move(fst));
            }
            if (snd.freq > 0) {
                queue.emplace(std::move(snd));
            }
        }

        return res;
    }
};
```