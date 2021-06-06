
# Problem
### LeetCode 133. Clone Graph
https://leetcode.com/problems/clone-graph

# Solution
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    Node* cloneGraph(Node* node) {

        if (!node) {
            return nullptr;
        }

        unordered_map<Node*, Node*> map;
        map[node] = new Node(node->val);

        queue<Node*> q;
        q.emplace(node);

        unordered_set<Node*> set;
        set.emplace(node);

        while (!q.empty()) {
            auto src = q.front();
            q.pop();

            for (auto dst : src->neighbors) {
                if (set.count(dst) == 0) {
                    map[dst] = new Node(dst->val);
                    q.emplace(dst);
                    set.emplace(dst);
                }
                map[src]->neighbors.emplace_back(map[dst]);
            }
        }

        return map[node];
    }
};
```
