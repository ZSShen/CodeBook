
# Problem
### LintCode 650. Find Leaves of Binary Tree
https://www.lintcode.com/problem/find-leaves-of-binary-tree/description

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
    vector<vector<int>> findLeaves(TreeNode* root) {

        /**
         *  Use post-order traversal. Also, classify a node using its height.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        unordered_map<int, vector<int>> map;
        int h = runPostOrder(root, map);

        vector<vector<int>> ans;
        for (int i = 1 ; i <= h ; ++i) {
            ans.emplace_back(move(map[i]));
        }
        return ans;
    }

private:
    int runPostOrder(
            TreeNode* root, unordered_map<int, vector<int>>& map) {

        if (!root) {
            return 0;
        }

        int l = runPostOrder(root->left, map);
        int r = runPostOrder(root->right, map);
        int h = max(l, r) + 1;

        map[h].emplace_back(root->val);
        return h;
    }
};
```