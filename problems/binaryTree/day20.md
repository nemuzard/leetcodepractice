### 654. Maximum Binary Tree
Link: [654. Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/description/)

**Idea**
- this problem is very similar to construct binary tree based on given inorde/postorder node
- The point is not find `max_val` for left and right, but the left tree and right tree

**Solution**
``` ccp
class Solution {
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        
        if(nums.size()==0) return NULL;

        int max = 0;
        int index = 0;
        for(int i  = 0; i<nums.size();i++){
            if(nums[i]>max){
                max = nums[i];
                index = i;
            }
        }

        TreeNode* root = new TreeNode(max);
        if(nums.size()==1) return root;
        
        // slice the array, left max is the left child and right is the right child
        vector<int> leftTree(nums.begin(),nums.begin()+index);
        vector<int> rightTree(nums.begin()+index+1,nums.end());        
        root->left = constructMaximumBinaryTree(leftTree);
        root->right = constructMaximumBinaryTree(rightTree);
        return root;

    }
};

```

Time Complexity: O(n**2)

### 617. Merge Two Binary Trees
Link: [617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/description/)

**Idea**
- `root->left` and `root->right` means entire left and right subtree
- add node->val
- each time pass the subtree to the recursive function,

**Solution**

```ccp
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        
        if(root1==NULL) return root2;
        if(root2==NULL) return root1;
        root1->val = root1->val+root2->val;
        root1->left = mergeTrees(root1->left, root2->left);
        root1->right = mergeTrees(root1->right, root2->right);
        return root1;

    }
};
```

Time complexity = O(n) where n = number of nodes in both trees

### 700. Search in a Binary Search Tree
Link: [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)

**Idea**
- Define stop condition: if root == null or root->val = target val, return the root
- if not, continue search the tree. The left side of the root has smaller value, and right side has greater val
- compare and decide where to go
- if not find, return null at the end.

**Solution**

```ccp
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        
        // stop condition. if we find the node->var = val will return here 
        if(root == NULL || root->val == val) return root;

        if(root->val > val) return searchBST(root->left, val);
        if(root->val < val) return searchBST(root->right, val);
        
        // no such subtree
        return NULL; 
    }
};

//iteration
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        while (root != NULL) {
            if (root->val > val) root = root->left;
            else if (root->val < val) root = root->right;
            else return root;
        }
        return NULL;
    }
}
```

Time Complexity: O(n)

### 98. Validate Binary Search Tree
Link: [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

**Idea**
- the `cur` becomes the new `maxNode` for the left subtree when recursing the Left subtree
- the `cur` becomes the new `minNode` for the right subtree when recusing the Right subtree
- because all nodes on the left are smaller then `cur` and all nodes on the right are greater than `cur` due to the property of the binary research tree

**Solution**

```ccp
class Solution {
private:
    bool check(TreeNode* cur, TreeNode* minNode, TreeNode* maxNode){
        if(!cur) return true;
        if(minNode && cur->val <= minNode->val) return false;
        if(maxNode && cur->val >= maxNode->val) return false;

        return check(cur->left,minNode,cur) && check(cur->right, cur, maxNode);
    }
public:
    bool isValidBST(TreeNode* root) {
        return check(root,nullptr, nullptr);
    }

};
```

Time Complexity: O(n)

