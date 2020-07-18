# Problem

### LeetCode 987. Vertical Order Traversal of a Binary Tree

https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/

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
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        map<int, map<int, set<int>>> map;
        runPreOrder(root, 0, 0, map);

        vector<vector<int>> ans;
        for (auto& outter : map) {
            vector<int> level;
            for (auto& inner : outter.second) {
                for (int elem : inner.second) {
                    level.emplace_back(elem);
                }
            }
            ans.emplace_back(move(level));
        }
        return ans;
    }

private:
    void runPreOrder(
            TreeNode* root, int x, int y,
            map<int, map<int, set<int>>>& map) {

        if (!root) {
            return;
        }

        map[x][y].emplace(root->val);
        runPreOrder(root->left, x - 1, y + 1, map);
        runPreOrder(root->right, x + 1, y + 1, map);
    }
};
```
