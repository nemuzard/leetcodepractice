### 235. Lowest Common Ancestor of a Binary Search Tree

Link: [235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

**Idea**
- according to the characteristics of a BFS
-  search left if smaller than cur->val, otherwise search right
-  if found, return cur


**Solution**

```ccp
class Solution {
public:
    TreeNode* traversal(TreeNode* cur,TreeNode*  p,TreeNode*  q){
        if(cur == NULL) return cur;
        if(cur->val>p->val && cur->val >q->val){
            TreeNode* left = traversal(cur->left,p,q);
            if(left!=NULL) return left;
        }
        if(cur->val<p->val && cur->val < q->val){
            TreeNode* right = traversal(cur->right,p,q);
            if(right!=NULL) return right;
        }

        return cur;

    }
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        return traversal(root,p,q);
    }
};

// iteration
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while(root) {
            if (root->val > p->val && root->val > q->val) {
                root = root->left;
            } else if (root->val < p->val && root->val < q->val) {
                root = root->right;
            } else return root;
        }
        return NULL;
    }
};
```

### 701. Insert into a Binary Search Tree
Link [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/description/)

**Idea**
- add new node at leaf position
- compare val and the val of each node to find where to add

**Solution**

```ccp
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == NULL){
            TreeNode* node = new TreeNode(val);
            return node;
        }

        if(root->val>val){
            root->left = insertIntoBST(root->left, val);

        }

        if(root->val<val) root->right = insertIntoBST(root->right,val);

        return root;
    }
};
```
