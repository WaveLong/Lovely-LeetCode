102. Binary Tree Level Order Traversal

Medium

Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```



return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>>ans;
        if(root == NULL)return ans;
        vector<int>tmp;
        queue<pnode>q;
        q.push(root);
        int cur = 1;
        int next = 0;
        while(!q.empty()){
            pnode t = q.front();
            q.pop();
            cur--;
            tmp.push_back(t->val);
            if(t->left != NULL){
                q.push(t->left);
                next++;
            }
            if(t->right != NULL){
                q.push(t->right);
                next++;
            }
            if(cur == 0){
                cur = next;
                next = 0;
                ans.push_back(tmp);
                tmp.clear();
            }
        }
        return ans;
    }
};
```

