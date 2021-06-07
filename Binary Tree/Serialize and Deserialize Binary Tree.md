# Problem

### LintCode 7. Serialize and Deserialize Binary Tree

https://www.lintcode.com/problem/serialize-and-deserialize-binary-tree/description

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
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         *
         *      3
         *     / \
         *    9   20
         *       /  \
         *      15   7
         *
         *   3, 9, #, #, 20, 15, #, #, 7, #, #
         */

        if (!root) {
            return "#";
        }

        return to_string(root->val) + "," +
                serialize(root->left) + "," +
                serialize(root->right);
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {

        stringstream stream(data);
        return helper(stream);
    }

private:
    TreeNode* helper(stringstream& stream) {

        string token;
        getline(stream, token, ',');

        if (token == "#") {
            return nullptr;
        }

        auto node = new TreeNode(stoi(token));
        node->left = helper(stream);
        node->right = helper(stream);
        return node;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```
