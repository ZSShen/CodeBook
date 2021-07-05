
# Problem
### LintCode 96. Partition List
https://www.lintcode.com/problem/partition-list/description

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
    ListNode* partition(ListNode* head, int x) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         */

        ListNode dummy_l, dummy_g;
        auto l = &dummy_l, g = &dummy_g;

        while (head) {
            if (head->val < x) {
                l = l->next = head;
            } else {
                g = g->next = head;
            }
            head = head->next;
        }

        g->next = nullptr;
        l->next = dummy_g.next;

        return dummy_l.next;
    }
};
```