
# Problem
### LeetCode 138. Copy List with Random Pointer
https://leetcode.com/problems/copy-list-with-random-pointer

# Solution
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;

    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         *
         *      A -> B -> C -> ...
         *
         *  Step 1. Generate a replicated node for each node and put that copy
         *  behind the original node.
         *
         *      A -> A+ -> B -> B+ -> C -> C+ -> ...
         *
         *  Step 2. For an orignal node, follow its random pointer.
         *  Then, the node next to the pointed node would be the one that the
         *  random pointer of the replicated node should point to.
         *
         *        random
         *      A ------> C -> C+
         *   => A+ -> C+
         *
         *      -----------------------
         *      |                     |
         *      |                     v
         *      A -> A+ -> B -> B+ -> C -> C+ -> ...
         *           |                      ^
         *           |                      |
         *           ------------------------
         *
         *  Step 3. Finally, we need to split the replicated list and the
         *  original list.
         */

        if (!head) {
            return nullptr;
        }

        auto curr = head;
        while (curr) {
            auto clone = new Node(curr->val);
            clone->next = curr->next;
            curr->next = clone;
            curr = clone->next;
        }

        curr = head;
        while (curr) {
            auto clone = curr->next;
            if (curr->random) {
                clone->random = curr->random->next;
            }
            curr = clone->next;
        }

        curr = head;
        auto res = curr->next;

        while (curr) {
            auto clone = curr->next;
            curr->next = clone->next;
            if (clone->next) {
                clone->next = clone->next->next;
            }
            curr = curr->next;
        }

        return res;
    }
};
```
