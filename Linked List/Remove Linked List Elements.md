
# Problem
### LeetCode 203. Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements

# Solution
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         */

        ListNode dummy;
        dummy.next = head;

        auto curr = head, pred = &dummy;
        while (curr) {
            auto succ = curr->next;
            if (curr->val == val) {
                pred->next = succ;
                delete curr;
            } else {
                pred = pred->next;
            }
            curr = succ;
        }

        return dummy.next;
    }
};
```
