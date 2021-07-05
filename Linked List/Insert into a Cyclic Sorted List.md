
# Problem
### LeetCode 708. Insert into a Sorted Circular Linked List
https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list

# Solution
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;

    Node() {}

    Node(int _val) {
        val = _val;
        next = NULL;
    }

    Node(int _val, Node* _next) {
        val = _val;
        next = _next;
    }
};
*/

class Solution {
public:
    Node* insert(Node* head, int val) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         *
         *  p    s
         *  3 -> 4 -> 1
         *
         *       p    s
         *  3 -> 4 -> 1
         *
         *  1. pred->val <= val && val <= succ->val
         *  2. pred->val > succ->val
         *      a. val <= succ->val (minimum)
         *      b. val >= pred->val (maximum)
         *
         *  3 all the node values are equal, but val is different:
         *      1 -> 1 -> 1
         *      val = 2
         */

        if (!head) {
            auto node = new Node(val);
            node->next = node;
            return node;
        }

        auto pred = head;
        auto succ = pred->next;

        do {
            if ((pred->val <= val && val <= succ->val) ||
                (pred->val > succ->val && val <= succ->val) ||
                (pred->val > succ->val && pred->val <= val)) {
                auto node = new Node(val);
                pred->next = node;
                node->next = succ;
                return head;
            }

            pred = succ;
            succ = succ->next;
        } while (pred != head);

        auto node = new Node(val);
        node->next = head->next;
        head->next = node;
        return head;
    }
};
```
