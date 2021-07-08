
# Problem
### LeetCode 382. Linked List Random Node
https://leetcode.com/problems/linked-list-random-node

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
    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    Solution(ListNode* head)
        : head(head) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */
    }

    /** Returns a random node's value. */
    int getRandom() {

        int count = 0, ans;
        auto curr = head;

        while (curr) {
            ++count;
            if (random() % count == 0) {
                ans = curr->val;
            }
            curr = curr->next;
        }

        return ans;
    }

private:
    ListNode* head;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(head);
 * int param_1 = obj->getRandom();
 */
```
