# Problem

### LeetCode 272. Closest Binary Search Tree Value II
https://leetcode.com/problems/closest-binary-search-tree-value-ii

# Solution
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> closestKValues(TreeNode* root, double target, int k) {

        /**
         *  TC: O(H + K), where
         *      H is the height of the tree
         *
         *  SC: O(H + K)
         *
         *  target = 19.
         *  k = 3
         *
         *          20
         *         /  \
         *       15    30
         *      /  \    \
         *    10    17   35
         *   /  \    \
         *  5   12    18
         *
         *
         *  pred: 20
         *  succ: 15, 17, 18
         *
         *  20 -> 15 -> 17 -> 18
         */

        stack<TreeNode*> preds;
        stack<TreeNode*> succs;

        while (root) {
            if (root->val >= target) {
                succs.emplace(root);
                root = root->left;
            } else {
                preds.emplace(root);
                root = root->right;
            }
        }

        vector<int> ans;

        for (int i = 0 ; i < k ; ++i) {
            if (preds.empty()) {
                ans.emplace_back(succs.top()->val);
                getSuccessors(succs);
                continue;
            }

            if (succs.empty()) {
                ans.emplace_back(preds.top()->val);
                getPredecessors(preds);
                continue;
            }

            auto pred = preds.top();
            auto succ = succs.top();

            double diff_p = abs(target - static_cast<double>(pred->val));
            double diff_s = abs(target - static_cast<double>(succ->val));

            if (diff_p <= diff_s) {
                ans.emplace_back(pred->val);
                getPredecessors(preds);
            } else {
                ans.emplace_back(succ->val);
                getSuccessors(succs);
            }
        }

        return ans;
    }

private:
    void getPredecessors(stack<TreeNode*>& preds) {

        auto curr = preds.top();
        preds.pop();

        if (curr) {
            curr = curr->left;
            while (curr) {
                preds.emplace(curr);
                curr = curr->right;
            }
        }
    }

    void getSuccessors(stack<TreeNode*>& succs) {

        auto curr = succs.top();
        succs.pop();

        if (curr) {
            curr = curr->right;
            while (curr) {
                succs.emplace(curr);
                curr = curr->left;
            }
        }
    }
};
```
