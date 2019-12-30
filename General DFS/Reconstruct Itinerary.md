
# Problem
### LintCode 1288. Reconstruct Itinerary
https://www.lintcode.com/problem/reconstruct-itinerary/description

# Solution
```c++

struct Record {
    string node;
    bool used;

    Record(const auto& node, bool used)
        : node(node), used(used)
    { }
};

class Solution {
public:
    vector<string> findItinerary(vector<vector<string>>& tickets) {

        unordered_map<string, vector<Record>> map;
        for (const auto& ticket : tickets) {
            map[ticket[0]].emplace_back(ticket[1], false);
        }

        for (auto& pair : map) {
            std::sort(pair.second.begin(), pair.second.end(),
                [] (const auto& lhs, const auto& rhs) {
                    return lhs.node < rhs.node;
                }
            );
        }

        vector<string> ans;
        ans.push_back("JFK");
        runBackTracking(1, tickets.size() + 1, "JFK", map, ans);

        return ans;
    }

private:
    bool runBackTracking(
        int c, int n, const auto& src, auto& map, auto& ans) {

        if (c == n) {
            return true;
        }

        auto& dsts = map[src];
        for (auto& dst : dsts) {
            if (dst.used) {
                continue;
            }

            dst.used = true;
            ans.emplace_back(dst.node);

            bool res = runBackTracking(c + 1, n, dst.node, map, ans);
            if (res) {
                return true;
            }

            ans.pop_back();
            dst.used = false;
        }

        return false;
    }
};
```
