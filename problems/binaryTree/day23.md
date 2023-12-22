### 669. Trim a Binary Search Tree
Link [669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/)

**Idea**

- delete nodes which values are not in [low, high]
- if a node does not in the range still need to check its children
_**Need to add more**_


**Solution**

```ccp
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        if(root==NULL) return NULL;
        // search right subtree of the node which is smaller than lower bound (since nodes in right subtree may within our bound)
        if(root->val<low){
            TreeNode* right = trimBST(root->right,low,high);
            return right;
        }
        if(root->val>high){
            TreeNode* left = trimBST(root->left,low,high);
            return left;
        }
        root->left = trimBST(root->left,low,high);
        root->right = trimBST(root->right,low,high);
        return root;
    }
};
```

### 108. Convert Sorted Array to Binary Search Tree
Link [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)

**Idea**

- given a sorted array, find middle position value be the root
- recursively call the function, if left>right return NULL
- root->left will use new range which is [left, mid-1] while root->right is [mid+1,right] (mid is the root)

**Solution**

```ccp

class Solution {
private:
    TreeNode* traversal(vector<int>& nums, int left, int right){
        if(left>right) return nullptr;
        int mid = left +(right-left)/2;
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = traversal(nums, left, mid-1);
        root->right = traversal(nums,mid+1,right);
        return root;

    }
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        TreeNode* root = traversal(nums, 0,nums.size()-1);
        return root;
    }
};
```

### 538. Convert BST to Greater Tree
Link [538. Convert BST to Greater Tree](https://leetcode.com/problems/convert-bst-to-greater-tree/description/)

**Idea**

- use postorder
- init pre = 0
- update cur->val += pre, and set pre = cur->val
- traverse left subtree
- if no such subtree, return
- It first continues the execution of the code for the current node (updating pre and traversing the left subtree), and only after that, it returns to the previous level of recursion.
    -  The order of operations within the function is as follows:
    -  1. Traverse right subtree.
       2.  Update cur->val and pre.
       3.  Traverse left subtree.
       4.   Return to the previous level of recursion.
     
**Solution**

```ccp
class Solution {
private:
    int pre = 0;
    void traversal(TreeNode* cur){
        if(cur==NULL) return;
        traversal(cur->right);
        cur->val += pre;
        pre = cur->val;
        traversal(cur->left);

    }
public:
    TreeNode* convertBST(TreeNode* root) {
        pre = 0;
        traversal(root);
        return root;
    }
};

```
