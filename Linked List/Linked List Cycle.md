
# Problem
### LeetCode 141. Linked List Cycle
https://leetcode.com/problems/linked-list-cycle

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
    bool hasCycle(ListNode *head) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         */

        if (!head) {
            return false;
        }

        auto slow = head, fast = head;

        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                return true;
            }
        }

        return false;
    }
};
```
