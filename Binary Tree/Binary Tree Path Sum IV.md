
# Problem
### LintCode 863. Binary Tree Path Sum IV
https://www.lintcode.com/problem/binary-tree-path-sum-iv/description

# Solution
```c++
class Solution {
public:

    /**
     * @param nums: a list of integers
     * @return: return an integer
     */
    int pathSum(vector<int> &nums) {
        // write your code here

        /**
         *  113 -> depth: 1, position: 1 -> 2 ^ 0 + 0 = 1 -> the 1st node
         *  215 -> depth: 2, position: 1 -> 2 ^ 1 + 0 = 3 -> the 3rd node
         *  ...
         *
         *  TODO: Clean the tree after resolving the answer.
         */

        if (nums.empty()) {
            return 0;
        }

        std::unordered_map<int, TreeNode*> map;
        for (int num : nums) {

            int depth = num / 100;
            num -= depth * 100;

            int position = num / 10;
            num -= position * 10;

            int index = pow(2, depth - 1) + (position - 1);

            map[index] = new TreeNode(num);
        }

        for (auto& pair : map) {
            int index = pair.first;
            auto curr = pair.second;

            int l_index = index << 1;
            if (map.count(l_index) == 1) {
                curr->left = map[l_index];
            }

            int r_index = l_index + 1;
            if (map.count(r_index) == 1) {
                curr->right = map[r_index];
            }
        }

        int ans = 0;
        runPreOrder(map[1], 0, ans);
        return ans;
    }

private:
    void runPreOrder(TreeNode* root, int sum, int& ans) {

        sum += root->val;

        if (!root->left && !root->right) {
            ans += sum;
        }

        if (root->left) {
            runPreOrder(root->left, sum, ans);
        }
        if (root->right) {
            runPreOrder(root->right, sum, ans);
        }

        sum -= root->val;
    }
};
```