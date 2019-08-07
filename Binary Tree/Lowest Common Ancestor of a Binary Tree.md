
# Problem
### LintCode 88. Lowest Common Ancestor of a Binary Tree
https://www.lintcode.com/problem/lowest-common-ancestor-of-a-binary-tree/description

# Solution
```c++
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */


class Solution {
public:
    /*
     * @param root: The root of the binary search tree.
     * @param A: A TreeNode in a Binary.
     * @param B: A TreeNode in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    TreeNode * lowestCommonAncestor(TreeNode * root, TreeNode * A, TreeNode * B) {
        // write your code here

        /**
         *  Postorder Traversal
         *  Note that this solution only works when A and B can be found.
         */

        if (!root) {
            return nullptr;
        }

        if (root == A || root == B) {
            return root;
        }

        auto l = lowestCommonAncestor(root->left, A, B);
        auto r = lowestCommonAncestor(root->right, A, B);

        if (l && r) {
            return root;
        }

        if (l) {
            return l;
        }

        if (r) {
            return r;
        }
    }
};
```