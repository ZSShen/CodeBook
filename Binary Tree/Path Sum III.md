
# Problem
### LeetCode 437. Path Sum III
https://leetcode.com/problems/path-sum-iii

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
    int pathSum(TreeNode* root, int target) {

        /**
         *  Similar to https://leetcode.com/problems/subarray-sum-equals-k
         *
         *  sum(i, j) = prefix(j) - prefix(i - 1) = target
         *  => prefix(i - 1) = prefix(j) - target
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        unordered_map<int, int> map;
        map[0] = 1;

        int ans = 0;
        runPreOrder(root, target, 0, map, ans);
        return ans;
    }

private:
    void runPreOrder(
            TreeNode* root, int target,
            int prefix, unordered_map<int, int>& map, int& ans) {

        if (!root) {
            return;
        }

        prefix += root->val;
        ans += map[prefix - target];

        ++map[prefix];
        runPreOrder(root->left, target, prefix, map, ans);
        runPreOrder(root->right, target, prefix, map, ans);
        --map[prefix];
    }
};
```