
# Problem
### LeetCode 148. Sort List
https://leetcode.com/problems/sort-list

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
    ListNode* sortList(ListNode* head) {

        /**
         *  TC: O(NlogN), where
         *      N is the number of nodes
         *
         *  SC: O(N)  The cost to maintain call stack
         */

        return merge(head, nullptr);
    }

private:
    ListNode* merge(ListNode* bgn, ListNode* end) {

        if (bgn == end) {
            return nullptr;
        }
        if (bgn->next == end) {
            bgn->next = nullptr;
            return bgn;
        }

        auto slow = bgn, fast = bgn;
        while (fast != end && fast->next != end) {
            slow = slow->next;
            fast = fast->next->next;
        }

        auto l = merge(bgn, slow);
        auto r = merge(slow, end);

        ListNode dummy;
        auto curr = &dummy;

        while (l && r) {
            if (l->val < r->val) {
                curr->next = l;
                l = l->next;
            } else {
                curr->next = r;
                r = r->next;
            }
            curr = curr->next;
        }

        while (l) {
            curr = curr->next = l;
            l = l->next;
        }
        while (r) {
            curr = curr->next = r;
            r = r->next;
        }

        return dummy.next;
    }
};
```
