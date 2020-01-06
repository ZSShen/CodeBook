# Problem

### LintCode 1506. All Nodes Distance K in Binary Tree

https://www.lintcode.com/problem/all-nodes-distance-k-in-binary-tree/description

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

struct MyTreeNode {
    MyTreeNode *parent, *left, *right;
    int val;

    MyTreeNode(int val)
        : parent(nullptr), left(nullptr), right(nullptr), val(val)
    { }
};


class Solution {
public:
    /**
     * @param root: the root of the tree
     * @param target: the target
     * @param K: the given K
     * @return: All Nodes Distance K in Binary Tree
     */
    vector<int> distanceK(TreeNode * root, TreeNode * target, int K) {
        // Write your code here

        MyTreeNode* new_target;
        auto new_root = runPreOrder(root, nullptr, target, new_target);

        vector<int> ans;
        runDfs(new_target, nullptr, K, ans);
        return ans;
    }

private:
    MyTreeNode* runPreOrder(
        TreeNode* root, MyTreeNode* parent,
        TreeNode* target, MyTreeNode*& new_target) {

        if (!root) {
            return nullptr;
        }

        auto curr = new MyTreeNode(root->val);
        curr->parent = parent;
        curr->left = runPreOrder(root->left, curr, target, new_target);
        curr->right = runPreOrder(root->right, curr, target, new_target);

        if (root == target) {
            new_target = curr;
        }

        return curr;
    }

    void runDfs(MyTreeNode* curr, MyTreeNode* pred, int K, auto& ans) {

        if (K == 0) {
            ans.push_back(curr->val);
            return;
        }

        if (curr->left && curr->left != pred) {
            runDfs(curr->left, curr, K - 1, ans);
        }
        if (curr->right && curr->right != pred) {
            runDfs(curr->right, curr, K - 1, ans);
        }
        if (curr->parent && curr->parent != pred) {
            runDfs(curr->parent, curr, K - 1, ans);
        }
    }
};
```
