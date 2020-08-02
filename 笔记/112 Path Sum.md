112. Path Sum

Easy

1277400FavoriteShare

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**

Given the below binary tree and `sum = 22`,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

**Solution**

dfs即可，注意简单的代码逻辑就不要拆分成单个函数，会增加运行时间

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
private:
    bool flag = false;
    int sum;
public:
    bool hasPathSum(TreeNode* root, int sum) {
        this->sum = sum;
        if(root)dfs(root, 0);
        return this->flag;
    }
    void dfs(TreeNode* root, int curSum){
        if(root == NULL)return;
        if(!(root->left || root->right) && curSum + root->val == this->sum){
            this->flag = true;
            return;
        }
        dfs(root->left, curSum+root->val);
        if(this->flag)return;
        dfs(root->right, curSum+root->val);
        if(this->flag)return;
    }
};
```

