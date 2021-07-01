
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
         */

        auto a = headA;
        auto b = headB;

        int la = 0;
        while (a) {
            ++la;
            a = a->next;
        }

        int lb = 0;
        while (b) {
            ++lb;
            b = b->next;
        }

        a = headA;
        b = headB;

        while (la > lb) {
            a = a->next;
            --la;
        }
        while (lb > la) {
            b = b->next;
            --lb;
        }

        while (a != b) {
            a = a->next;
            b = b->next;
        }

        return a;
    }
};
```
