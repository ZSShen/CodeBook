
# Problem
### LeetCode 142. Linked List Cycle II
https://leetcode.com/problems/linked-list-cycle-ii

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
    ListNode *detectCycle(ListNode *head) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         *
         *        a    X  b  Y
         *  ------------------
         *             |     |
         *             |     |
         *             |     |
         *             -------
         *           c
         *
         *  The starting point of the cycle is X
         *  The tortoise and the hare meet at Y
         *
         *  The # of steps that the tortoise has taken is a + b
         *  The # of steps that the hare has taken is a + b + c + b
         *
         *  The # of steps taken by the hare is twice the # of steps
         *  taken by the tortoise
         *
         *  2 * (a + b) = a + b + c + b
         *  => a + b = c + b
         *  => a = c
         *
         */

        if (!head) {
            return nullptr;
        }

        auto slow = head, fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                break;
            }
        }

        if (!fast->next || !fast->next->next) {
            return nullptr;
        }

        slow = head;
        while (slow != fast) {
            slow = slow->next;
            fast = fast->next;
        }

        return slow;
    }
};
```
