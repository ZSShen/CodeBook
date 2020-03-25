
# Problem
### LintCode 103. Linked List Cycle II
https://www.lintcode.com/problem/linked-list-cycle-ii/description

# Solution
```c++
/**
 * Definition of singly-linked-list:
 * class ListNode {
 * public:
 *     int val;
 *     ListNode *next;
 *     ListNode(int val) {
 *        this->val = val;
 *        this->next = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param head: The first node of linked list.
     * @return: The node where the cycle begins. if there is no cycle, return null
     */
    ListNode * detectCycle(ListNode * head) {
        // write your code here

        /**
         *  New explanation
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
         *  2 * (a + b) = a + b + c + b
         *  => a + b = c + b
         *  => a = c
         *
         */

        /**
         *
         *                     k - j - i <--- k
         *                     |       |
         *                     l       h
         *                     |       |
         *     a - b - c - d - e - f - g
         *
         *   Length of the prefix: X
         *   Length of the cycle: Y
         *   2 Pointers meet at the kth node.
         *
         *     t = X + nY + k
         *    2t = X + mY + k
         *
         *  => 2X + 2nY + 2k = X + mY + k
         *  => X + k = (m - 2n)Y
         *
         */

        auto slow = head;
        auto fast = head;

        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                break;
            }
        }

        if (!fast || !fast->next) {
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
