
# Problem
### LeetCode 1650. Lowest Common Ancestor of a Binary Tree III
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii

# Solution
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* parent;
};
*/

class Solution {
public:
    Node* lowestCommonAncestor(Node* p, Node * q) {

        /**
         *  TC: O(H), where
         *      H is the height of the tree
         *
         *  SC: O(H)
         */

        unordered_set<Node*> set;
        while (p) {
            set.emplace(p);
            p = p->parent;
        }

        while (q) {
            if (set.count(q) == 1) {
                return q;
            }
            q = q->parent;
        }

        return nullptr;
    }
};
```