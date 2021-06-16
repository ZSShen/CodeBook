
# Problem
### LeetCode 332. Reconstruct Itinerary
https://leetcode.com/problems/reconstruct-itinerary

# Solution
```c++
class Solution {
public:
    vector<string> findItinerary(vector<vector<string>>& tickets) {

        /**
         *  TC: O(D ^ E), where
         *      D is the averaged number of outgoing flight from a city
         *      E is the number of flights
         *
         *  SC: O(V + E), where
         *      V is the number of cities
         */

        unordered_map<string, vector<pair<string, bool>>> graph;
        int n = tickets.size();

        for (const auto& ticket : tickets) {
            const auto& s = ticket[0];
            const auto& t = ticket[1];
            graph[s].push_back({t, false});
        }

        for (auto& pair : graph) {
            auto& edges = pair.second;
            sort(edges.begin(), edges.end());
        }

        vector<string> seq;
        seq.push_back("JFK");
        dfs(0, n, "JFK", graph, seq);
        return seq;
    }

private:
    bool dfs(
        int count, int n,
        const string& src,
        unordered_map<string, vector<pair<string, bool>>>& graph,
        vector<string>& seq) {

        if (count == n) {
            return true;
        }

        for (auto& edge : graph[src]) {
            if (edge.second) {
                continue;
            }

            edge.second = true;
            seq.push_back(edge.first);

            bool res = dfs(count + 1, n, edge.first, graph, seq);
            if (res) {
                return true;
            }

            seq.pop_back();
            edge.second = false;
        }

        return false;
    }
};
```
