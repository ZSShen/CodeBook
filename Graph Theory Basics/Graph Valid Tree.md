
# Problem
### LeetCode 261. Graph Valid Tree
https://leetcode.com/problems/graph-valid-tree/solution

# Solution
```c++

class DSU {
public:
    DSU(int n)
        : n(n), parent(n) {

        for (int i = 0 ; i < n ; ++i) {
            parent[i] = i;
        }
    }

    int find(int x) {
        if (x == parent[x]) {
            return x;
        }

        return parent[x] = find(parent[x]);
    }

    void merge(int x, int y) {
        int px = find(x);
        int py = find(y);

        if (px != py) {
            --n;
            parent[px] = py;
        }
    }

    int query() {
        return n;
    }

private:
    int n;
    vector<int> parent;
};


class Solution {
public:
    bool validTree(int n, vector<vector<int>>& edges) {

        /**
         *  TC: O(N * ack(N)), where
         *      N is the number of nodes
         *      ack(N) is the Ackerman function
         *
         *  SC: O(N)
         *
         *  We can use the data structure, disjoint set and union find, to check
         *  if a graph is a valid tree. If the graph is a valid tree, it should
         *  fulfill the following 2 requirements.
         *
         *   1. Suppose the number of nodes is n, then the number of edges
         *      should be n - 1.
         *
         *   2. The graph has only one connected component.
         */

        int e = edges.size();
        if (n != e + 1) {
            return false;
        }

        DSU dsu(n);
        for (const auto& edge : edges) {
            dsu.merge(edge[0], edge[1]);
        }

        return dsu.query() == 1;
    }
};
```