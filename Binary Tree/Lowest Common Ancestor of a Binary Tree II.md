
# Problem
### LeetCode Lowest Common Ancestor of a Binary Tree II
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-ii

# Solution
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

struct Record {
    bool find_p = false;
    bool find_q = false;
    TreeNode* lca = nullptr;
};


class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {

        /**
         *  Use post-order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        auto rtn = helper(root, p, q);
        return rtn.lca;
    }

private:
    Record helper(TreeNode* root, TreeNode* p, TreeNode* q) {

        if (!root) {
            return Record();
        }

        auto l = helper(root->left, p, q);
        if (l.lca) {
            return l;
        }

        auto r = helper(root->right, p, q);
        if (r.lca) {
            return r;
        }

        Record rtn;
        rtn.find_p = l.find_p || r.find_p || root == p;
        rtn.find_q = l.find_q || r.find_q || root == q;

        if (rtn.find_p && rtn.find_q) {
            rtn.lca = root;
        }
        return rtn;
    }
};
```