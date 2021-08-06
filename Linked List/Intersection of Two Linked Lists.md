
# Problem
### LeetCode 160. Intersection of Two Linked Lists
https://leetcode.com/problems/intersection-of-two-linked-lists

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {

        /**
         *  TC: O(M + N), where
         *      M is the number of nodes of list A
         *      N is the number of nodes of list B
         *
         *  SC: O(1)
         *
         *  A ________
         *            \
         *             \__________ C
         *             /
         *      B ____/
         *
         *  a + c + b = b + c + a
         */

        auto a = headA, b = headB;

        while (a != b) {
            a = a ? a->next : headB;
            b = b ? b->next : headA;
        }

        return a;
    }
};
```
