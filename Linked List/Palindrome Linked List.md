
# Problem
### LeetCode 234. Palindrome Linked List
https://leetcode.com/problems/palindrome-linked-list

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
    bool isPalindrome(ListNode* head) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         */

        if (!head || !head->next) {
            return true;
        }

        if (!head->next->next) {
            return head->val == head->next->val;
        }

        // Find the middle point of the list.
        auto slow = head, fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        // Reverse the right portion.
        auto pred = slow, curr = slow->next;
        int count = 0;
        while (curr) {
            auto succ = curr->next;
            curr->next = pred;
            pred = curr;
            curr = succ;
            ++count;
        }

        auto left = head, right = pred;
        bool is_palin = true;
        for (int i = 0 ; i < count ; ++i) {
            if (left->val != right->val) {
                is_palin = false;
                break;
            }
            left = left->next;
            right = right->next;
        }

        // Restore the right portion.
        curr = pred;
        pred = nullptr;
        for (int i = 0 ; i < count ; ++i) {
            auto succ = curr->next;
            curr->next = pred;
            pred = curr;
            curr = succ;
        }
        slow->next = pred;

        return is_palin;
    }
};
```
