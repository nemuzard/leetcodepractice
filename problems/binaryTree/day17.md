### Note on depth and height
- `height`：
  - Height of a Node: The height of a node in a binary tree is the number of edges on the longest path _from the node to a leaf. A leaf node has a height of 0._
  - Height of a Tree: The height of the tree is the height of its root node. This is the longest path from the root to any leaf.
- Need to use **DFS** or **PostOrder Traversal**
  - why? -- Because binary tree has recursive order, if we want to know the height of the tree, we should know the height of its left subtree and right subtree, and find max+1 --> this add 1 is where we put the mid to the end which is **postorder**
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
### 257. Binary Tree Paths
Link: [257. Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/description/)

**Idea**

```ccp
input: vector<int>& str
       TreeNode* cur
       vector<string>& res 
```
- traverse the tree path by path, when arrives at the leaf node, it will finish other recursive call which then will step back
- construct the string after hitting the leaf which is cur->left and cur->right both are NULL
  - add the path to our result ( but need to do some work on path to satisfy format requirements  

**Solution**
```ccp
class Solution {
public:
    void traversal(TreeNode* cur, vector<int>& path, vector<string>& result){
        // stop condition 
        if(cur==NULL) return;
        // mid 
        path.push_back(cur->val);
        // finished adding a single path
        if(cur->left==NULL && cur->right==NULL){
            string s = "";
            for(int i=0;i<path.size()-1;i++){
                s += to_string(path[i]);
                if(i<path.size()-1){
                    s+="->";
                }
            }
            s+=to_string(path[path.size()-1]);
            result.push_back(s);
        }
        if(cur->left){
            traversal(cur->left,path,result);
            path.pop_back();
        }
        if(cur->right){
            traversal(cur->right,path,result);
            path.pop_back();
        }
        
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> res;
        vector<int> path;
        if(root==NULL) return res;
        traversal(root,path,res);
        return res;
    }
};
```

### 404. Sum of Left Leaves
Link: [404. Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/description/)

**Idea**
- key point is the left leaf condition: `root->left && !root->left->left && !root->left->right`
- only parent if a node is a left leaf.
- for each root->left and root->right we have to reach the left node and then calculate the sum

**Solution**

```ccp
// postorder 
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if(root==NULL) return 0; // if left node is null then the sum of left node must be 0
        int left = sumOfLeftLeaves(root->left);
        
        if(root->left==NULL && root->right==NULL) return 0; // for each "root" we collect its left leaf, so we do not want leaves to be a "root" since they do not have any children so return 0 
        //left node
        if(root->left!=NULL && root->left->left==NULL && root->left->right==NULL){
            left = root->left->val;
        }
        int right_left = sumOfLeftLeaves(root->right);
        int sum = left + right_left;
        return sum;

    }
};
```


