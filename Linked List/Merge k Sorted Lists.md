
# Problem
### LeetCode 23. Merge k Sorted Lists
https://leetcode.com/problems/merge-k-sorted-lists

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {

        /**
         *  TC: O(NlogK), where
         *      N is the total number of nodes
         *      K is the number of lists
         *
         *  SC: O(logK)  The cost to maintain call stack
         */

        return helper(0, lists.size() - 1, lists);
    }

private:
    ListNode* helper(int bgn, int end, vector<ListNode*>& lists) {

        if (bgn > end) {
            return nullptr;
        }
        if (bgn == end) {
            return lists[bgn];
        }

        int mid = (bgn + end) >> 1;
        auto l = helper(bgn, mid, lists);
        auto r = helper(mid + 1, end, lists);

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
