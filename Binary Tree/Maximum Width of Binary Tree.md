
# Problem
### LintCode 1101. Maximum Width of Binary Tree
https://www.lintcode.com/problem/maximum-width-of-binary-tree/description

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


struct Record {
    TreeNode* node;
    int label;

    Record(TreeNode* node, int label)
      : node(node), label(label)
    { }
};


class Solution {
public:
    /**
     * @param root: the root
     * @return: the maximum width of the given tree
     */
    int widthOfBinaryTree(TreeNode * root) {
        // Write your code here

        // Level Order Traversal + Tree Label

        if (!root) {
            return 0;
        }

        int width = 0;

        std::queue<Record> queue;
        queue.push(Record(root, 1));

        while (!queue.empty()) {

            int max = INT_MIN;
            int min = INT_MAX;
            int size = queue.size();

            for (int i = 0 ; i < size ; ++i) {
                auto rec = queue.front();
                queue.pop();

                auto node = rec.node;
                int label = rec.label;

                max = std::max(max, label);
                min = std::min(min, label);

                if (node->left) {
                    queue.push(Record(node->left, label * 2));
                }
                if (node->right) {
                    queue.push(Record(node->right, label * 2 + 1));
                }
            }

            width = std::max(width, max - min + 1);
        }

        return width;
    }
};
```