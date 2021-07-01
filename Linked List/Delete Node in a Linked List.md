
# Problem
### LeetCode 237. Delete Node in a Linked List
https://leetcode.com/problems/delete-node-in-a-linked-list

# Solution
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         */

        auto pred = node;
        auto curr = pred->next;

        while (curr->next) {
            pred->val = curr->val;
            pred = curr;
            curr = curr->next;
        }
        pred->val = curr->val;

        delete curr;
        pred->next = nullptr;
    }
};
```
