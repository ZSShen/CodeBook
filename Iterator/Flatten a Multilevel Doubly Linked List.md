
# Problem
### LeetCode 430. Flatten a Multilevel Doubly Linked List
https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list

# Solution
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* prev;
    Node* next;
    Node* child;
};
*/

class Solution {
public:
    Node* flatten(Node* head) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        if (!head) {
            return head;
        }

        stack<Node*> stk;
        stk.emplace(head);

        Node dummy;
        auto prev = &dummy;

        while (!stk.empty()) {
            auto curr = stk.top();
            stk.pop();

            while (curr) {
                prev->next = curr;
                curr->prev = prev;
                prev = curr;

                if (curr->child) {
                    stk.emplace(curr->next);
                    stk.emplace(curr->child);
                    curr->child = nullptr;
                    break;
                }

                curr = curr->next;
            }
        }

        dummy.next->prev = nullptr;
        return dummy.next;
    }
};
```