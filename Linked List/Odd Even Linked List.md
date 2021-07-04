
# Problem
### LeetCode 328. Odd Even Linked List
https://leetcode.com/problems/odd-even-linked-list

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
    ListNode* oddEvenList(ListNode* head) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(1)
         */

        if (!head || !head->next) {
            return head;
        }

        ListNode dummy_odd, dummy_even;
        auto odd = &dummy_odd, even = &dummy_even;

        int index = 1;
        while (head) {
            auto succ = head->next;

            if (index % 2 == 0) {
                even->next = head;
                even = even->next;
                even->next = nullptr;
            } else {
                odd->next = head;
                odd = odd->next;
                odd->next = nullptr;
            }

            head = succ;
            ++index;
        }

        odd->next = dummy_even.next;
        return dummy_odd.next;
    }
};
```
