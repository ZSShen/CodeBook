
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
         *
         *  A ________
         *            \
         *             \__________ C
         *             /
         *      B ____/
         *
         *  a + c + b = b + c + a
         */

        auto cp = p, cq = q;

        while (cp != cq) {
            cp = cp ? cp->parent : q;
            cq = cq ? cq->parent : p;
        }

        return cp;
    }
};
```