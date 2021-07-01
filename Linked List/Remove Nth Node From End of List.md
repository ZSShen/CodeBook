
# Problem
### LeetCode 19. Remove Nth Node From End of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         *
         *  Delete a normal node
         *
         *  1->2->3->4->5
         *  n = 2
         *
         *  l     r
         *  1->2->3->4->5
         *
         *           l     r
         *  1->2->3->4->5  nil
         *
         *  1->2->3->5
         *
         *  Delete a head node
         *
         *  1->2->3
         *  n = 3
         *
         *  l       r
         *  1->2->3 nil
         *
         *  2->3
         */

        auto l = head;
        auto p = head;
        auto r = head;

        for (int i = 0 ; i < n ; ++i) {
            r = r->next;
        }

        while (r) {
            r = r->next;
            p = l;
            l = l->next;
        }

        p->next = l->next;
        head = (l != head) ? head : head->next;
        delete l;
        return head;
    }
};
```
