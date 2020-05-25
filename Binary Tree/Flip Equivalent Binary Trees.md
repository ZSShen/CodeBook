
# Problem
### LeetCode 951. Flip Equivalent Binary Trees
https://leetcode.com/problems/flip-equivalent-binary-trees/

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
    bool flipEquiv(TreeNode* root1, TreeNode* root2) {
        return runPreOrder(root1, root2);
    }

private:
    bool runPreOrder(TreeNode* sub, TreeNode* ref) {

        if (!sub && !ref) {
            return true;
        }
        if ((sub && !ref) || (!sub && ref)) {
            return false;
        }
        if (sub->val != ref->val) {
            return false;
        }

        return (runPreOrder(sub->left, ref->left) &&
                runPreOrder(sub->right, ref->right)) ||
               (runPreOrder(sub->left, ref->right) &&
                runPreOrder(sub->right, ref->left));
    }
};
```