# Problem

### LeetCode 105. Construct Binary Tree from Preorder and Inorder Traversal
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {

        /**
         *  TC: O(NlogN), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         *
         *  PreOrder: Root (left Branch) (Right Branch)
         *  InOrder : (Left Branch) Root (Right Branch)
         *
         *       1                    T     L        R
         *     /   \        PreOrder: 1, 2, 4, 5, 3, 6, 7
         *    2     3                    -------  -------
         *   / \   / \                   L     T     R
         *  4   5 6   7     InOrder : 4, 2, 5, 1, 6, 3, 7
         *                            -------     -------
         */

        int n = preorder.size();
        return helper(preorder, inorder, {0, n - 1}, {0, n - 1});
    }

private:
    TreeNode* helper(
            const vector<int>& preorder, const vector<int>& inorder,
            pair<int, int> pre_index, pair<int, int> in_index) {

        int in_bgn = in_index.first, in_end = in_index.second;
        if (in_bgn > in_end) {
            return nullptr;
        }
        if (in_bgn == in_end) {
            return new TreeNode(inorder[in_bgn]);
        }

        int pre_bgn = pre_index.first, pre_end = pre_index.second;
        int val = preorder[pre_bgn];

        int i;
        for (i = in_bgn ; i <= in_end ; ++i) {
            if (inorder[i] == val) {
                break;
            }
        }

        auto root = new TreeNode(val);

        root->left = helper(preorder, inorder,
                            {pre_bgn + 1, pre_bgn + i - in_bgn},
                            {in_bgn, i - 1});

        root->right = helper(preorder, inorder,
                             {pre_bgn + i - in_bgn + 1, pre_end},
                             {i + 1, in_end});
        return root;
    }
};
```

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        unordered_map<int, int> map;
        int n = inorder.size();
        for (int i = 0 ; i < n ; ++i) {
            map[inorder[i]] = i;
        }

        return helper(preorder, inorder, {0, n - 1}, {0, n - 1}, map);
    }

private:
    TreeNode* helper(
            const vector<int>& preorder, const vector<int>& inorder,
            pair<int, int> pre_index, pair<int, int> in_index,
            unordered_map<int, int>& map) {

        int in_bgn = in_index.first, in_end = in_index.second;
        if (in_bgn > in_end) {
            return nullptr;
        }
        if (in_bgn == in_end) {
            return new TreeNode(inorder[in_bgn]);
        }

        int pre_bgn = pre_index.first, pre_end = pre_index.second;
        int val = preorder[pre_bgn];

        // Find the root node index of the in-order vector.
        int in_mid = map[val];

        auto root = new TreeNode(val);

        root->left = helper(preorder, inorder,
                            {pre_bgn + 1, pre_bgn + in_mid - in_bgn},
                            {in_bgn, in_mid - 1}, map);

        root->right = helper(preorder, inorder,
                             {pre_bgn + in_mid - in_bgn + 1, pre_end},
                             {in_mid + 1, in_end}, map);

        return root;
    }
};
```