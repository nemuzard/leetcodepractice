### 226. Invert Binary Tree
Link: [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)
```ccp
      root                                root
  left     right          ---->      right      left 
l1    l2  r1    r2                  r1   r2    l1   l2 
                                             
      root                                 |
 right     left                    <------                
r2   r1   l2   l1
```

**Idea**
Recursion
1. first swap left subtree and right subtree
2. then swap their children.
3. each recursive function call will update root to either left or right child

Iteration
1. init a stack
2. push the root to the stack: always keep the top be the current root
3. while the stack is not empty
4. swap its left and right
5. if node->right or left is not null, push it to the stack

**Solution**
``` ccp
//recursion
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        
        if(root == NULL) return root;
        swap(root->left,root->right);
        invertTree(root->right);
        invertTree(root->left);
        return root;
    }
};
// iteration
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        
        if(root == NULL) return root;
        stack<TreeNode*> st;
        st.push(root);

        while(!st.empty()){
            TreeNode* cur = st.top();
            st.pop();
            swap(cur->left,cur->right);
            if(cur->left) st.push(cur->left);
            if(cur->right) st.push(cur->right);
        }

        return root;
    }

};
```

### 101. Symmetric Tree
Link:[ 101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/submissions/)

**Idea**
1. if root is null --> is symmetric
2. at each level we compare left.right and right.left and left.left and right.right
3. if both left and right are null, return true
4. if their values are not equal or one of them is null, then return false

**Solution**
```ccp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        
        return isMirror(root->left,root->right);
        
    }

    bool isMirror(TreeNode* left, TreeNode*right){
        if(!left && !right ) return true; // empty
        if(!left||!right||left->val!=right->val) return false;

        return isMirror(left->left, right->right)&& isMirror(left->right, right->left);
    }
};
```

Time Complexity: O(n)
