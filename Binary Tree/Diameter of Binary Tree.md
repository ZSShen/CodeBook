
# Problem
### LintCode 1181. Diameter of Binary Tree
https://www.lintcode.com/problem/diameter-of-binary-tree/description

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
    int diameterOfBinaryTree(TreeNode* root) {

        /**
         *  Use post-order traversal.
         *
         *  To get the diameter of the subtree rooted by a node R, we can divide
         *  the diamter into 2 segments, each of which can be calculated from
         *  either the left branch or the right branch of R. Then, we merge
         *  these 2 segments to form the diameter. Please note that the segment
         *  is essentially the maximum depth of a tree. Therefore, we collect
         *  the maximum depths from both branches and combine them to form
         *  a diameter path.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        int opt = 0;
        runPostOrder(root, opt);
        return opt;
    }

private:
    int runPostOrder(TreeNode* root, int& opt) {

        if (!root) {
            return 0;
        }

        int l = runPostOrder(root->left, opt);
        int r = runPostOrder(root->right, opt);
        opt = max(opt, l + r);
        return max(l, r) + 1;
    }
};
```