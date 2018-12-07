```c
// 网上抄的 vector操作太反人类了！
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
public:
    vector<TreeNode*> *DFSTrees(int start, int end){
        vector<TreeNode*> *subTree = new vector<TreeNode*>();
        if (start > end) {
            subTree->push_back(NULL);
            return subTree;
        }
        for (int i = start; i <= end; i++){
            vector<TreeNode*> *leftTree = DFSTrees(start, i-1);
            vector<TreeNode*> *rightTree = DFSTrees(i+1, end);
            for (int j = 0; j < leftTree->size(); j++){
                for (int k = 0; k < rightTree->size(); k++){
                    TreeNode *node = new TreeNode(i);
                    node->left = (*leftTree)[j];
                    node->right = (*rightTree)[k];
                    subTree->push_back(node);
                }
            }
        }
        return subTree;
    }
    vector<TreeNode*> generateTrees(int n) {
        if (n == 0){
            vector<TreeNode*> node;
            return node;
        }
        return *DFSTrees(1, n);
    }
};
```
