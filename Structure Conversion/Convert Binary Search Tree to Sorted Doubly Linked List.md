
# Problem
### LeetCode 426. Convert Binary Search Tree to Sorted Doubly Linked List
https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list

# Solution
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/

class Solution {
public:
    Node* treeToDoublyList(Node* root) {

        /**
         *  Run in-order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        if (!root) {
            return nullptr;
        }

        Node *pred = nullptr, *head = nullptr;

        helper(root, pred, head);
        head->left = pred;
        pred->right = head;

        return head;
    }

private:
    void helper(Node* root, Node*& pred, Node*& head) {

        if (!root) {
            return;
        }

        helper(root->left, pred, head);

        if (pred) {
            pred->right = root;
            root->left = pred;
        }
        pred = root;

        if (!head) {
            head = root;
        }

        helper(root->right, pred, head);
    }
};
```