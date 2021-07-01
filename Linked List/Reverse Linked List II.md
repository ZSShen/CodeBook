
# Problem
### LeetCode 92. Reverse Linked List II
https://leetcode.com/problems/reverse-linked-list-ii/submissions

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
    ListNode* reverseBetween(ListNode* head, int m, int n) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         *
         *    first
         *      |    m         n
         *      1 -> 2 -> 3 -> 4 -> 5
         *           |
         *         second
         *                   prev  curr
         *      1 <- 2 <- 3 <- 4 -> 5
         *
         *      first->next = prev
         *      second->next = curr
         */

        ListNode dummy;
        dummy.next = head;

        // Find the (m-1)th node.
        auto first = &dummy;
        for (int i = 0 ; i < m - 1 ; ++i) {
            first = first->next;
        }

        // Reverse the internal segment.
        auto tail = first->next;
        ListNode* pred = nullptr;
        auto curr = tail;
        for (int i = m ; i <= n ; ++i) {
            auto succ = curr->next;
            curr->next = pred;
            pred = curr;
            curr = succ;
        }

        first->next = pred;
        tail->next = curr;

        return dummy.next;
    }
};
```
