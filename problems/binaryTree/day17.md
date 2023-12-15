### Note on depth and height
- `height`：
  - Height of a Node: The height of a node in a binary tree is the number of edges on the longest path _from the node to a leaf. A leaf node has a height of 0._
  - Height of a Tree: The height of the tree is the height of its root node. This is the longest path from the root to any leaf.
- Need to use **DFS** or **PostOrder Traversal**
  - why? -- because binary tree has recursive order, if we want to know the height of the tree, we should know the height of its left subtree and right subtree, and find max+1 --> this add 1 is where we put the mid to the end which is **postorder**
- `depth `
  - The depth of a node in a binary tree is defined as the number of edges from the root node to the given node。 It is essentially the "level" at which the node exists in the tree.
  - Depth is Root-Dependent: Since depth is measured from the root downwards, you need to start at the root and work your way down the tree (hence preorder traversal).   




### 110. Balanced Binary Tree
Link: [110. Balanced Binary Tree]() \
**Idea**
- each function call, we return the _height_ which is defined as the maximum depth of any leaf node from the root node of the binary tree
- For each function call we will calculate the left height and right height, and calculate their difference, if greater than 1, then it is not a balanced tree, so return -1
- if returned `int = -1` , then we know it is not a balanced binary tree. so return `false`

**Solution**

```ccp
class Solution {
public:
    int checkHeight(TreeNode* cur){
        if(cur==NULL) return 0 ;
        
        int left = checkHeight(cur->left);
        if(left == -1) return -1;          // left and right can equal to -1 if abs(left-right) > 1 --> not balanced binary tree

        int right = checkHeight(cur->right);
        if(right == -1 ) return -1;

        if(abs(left-right) > 1) return -1;

        return max(left,right) +1; //This is where we calculate the height of the binary tree        
    }

    bool isBalanced(TreeNode* root) {
        return checkHeight(root)!=-1;
    }
};
```


