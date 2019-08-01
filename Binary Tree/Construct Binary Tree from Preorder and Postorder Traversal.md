# Problem

### LeetCode 889. Construct Binary Tree from Preorder and Postorder Traversal

https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/

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
class Solution {
public:
    TreeNode* constructFromPrePost(vector<int>& pre, vector<int>& post) {

        /**
            PreOrder : Root (Left Branch) (Right Branch)
            PostOrder: (Left Branch) (Right Branch) Root

                                          *
                1                      T  P  L        R
              /   \         PreOrder : 1, 2, 4, 5, 3, 6, 7
             2     3                      -------  -------
            / \   / \                     L  P     R     T
           4   5 6   7      PostOrder: 4, 5, 2, 6, 7, 3, 1
                                       -------  -------
        */

        int num_pre = pre.size();
        int num_post = post.size();

        if (num_pre == 0 || num_post == 0 || num_pre != num_post) {
            return nullptr;
        }

        return buildTree(pre, 0, num_pre - 1, post, 0, num_post - 1);
    }

private:
    TreeNode* buildTree(
            const auto& pre, int pre_bgn, int pre_end,
            const auto& post, int post_bgn, int post_end) {

        if (pre_bgn > pre_end) {
            return nullptr;
        }

        if (pre_bgn == pre_end) {
            return new TreeNode(pre[pre_bgn]);
        }

        int root_val = pre[pre_bgn];
        int pivot = pre[pre_bgn + 1];

        int mid;
        for (mid = post_bgn ; mid <= post_end ; ++mid) {
            if (post[mid] == pivot) {
                break;
            }
        }
        ++mid;

        int left_range = mid - post_bgn;

        auto root = new TreeNode(root_val);
        root->left = buildTree(
            pre, pre_bgn + 1, pre_bgn + left_range,
            post, post_bgn, mid - 1);
        root->right = buildTree(
            pre, pre_bgn + 1 + left_range, pre_end,
            post, mid, post_end - 1);

        return root;
    }
};
```
