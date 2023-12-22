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
### 450. Delete Node in a BST
Link [450. Delete Node in a BST]()

**Idea** \
5 cases:
1. not find, return null
2. left and right are not null
   - delete the node and put its left tree to  be the child of the lead node of the target node's leftmost child on the right subtree,
4. left is not null and right is null
5. right is not null and left is null
6. left and right null

**Solution**

```ccp

class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        // Tree is null or ..
        if(root == NULL) return NULL;// target node not found

        if(root->val == key) {
            if(root->left == NULL && root->right == NULL){
                delete root;
                return nullptr; // this is return to the previous level of the tree
            }else if(root->left && !root->right){
                auto retNode = root->left;
                delete root;
                return retNode; // return left tree to the previous level
            }else if(root->right && !root->left){
                auto retNode = root->right;
                delete root;
                return retNode;
            }else{
                // left and right are not NULL 
                TreeNode* cur = root->right; // we want to reach the leftmost node of the right subtree
                while(cur->left!=NULL) cur = cur->left; // arrived
                cur->left = root->left; // make cur be the new parent 
                TreeNode* tmp = root; // save root node
                root = root->right; // return old right child of the root as new root
                delete tmp;
                return root;
            }

        }
        if(root->val > key) root->left = deleteNode(root->left,key);
        if(root->val < key) root->right = deleteNode(root->right, key);
        return root;
    }
};
```
