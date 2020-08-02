94. Binary Tree Inorder Traversal

Medium

Given a binary tree, return the *inorder* traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

**Solution**

递归写法没问题。注意非递归写法，设置一个工作指针

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
typedef TreeNode* pnode;
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<pnode>s;
        vector<int>path;
        pnode cur = root;
        while(cur != NULL || !s.empty()){
            while(cur != NULL){
                s.push(cur);
                cur = cur->left;
            }
            if(!s.empty()){
                cur = s.top();
                s.pop();
                path.push_back(cur->val);
                cur = cur->right;
            }
        }
        return path;
    }
};
```

