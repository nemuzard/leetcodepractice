### 104. Maximum Depth of Binary Tree
Link: [104. Maximum Depth of Binary Tree]()

**Idea**

- each time you go to either left or right child, means you are lower one level, i.e go deeper --> depth+1
- we return the max depth which is the depth of the entire binary tree

**Solution**
```ccp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==NULL) return 0;
        int left = maxDepth(root->left) + 1;
        int right = maxDepth(root->right) + 1;

        return max(left,right);
    }
};

```

**Need to Understand this**

``` ccp
class Solution {
public:
    int result;
    void getDepth(TreeNode* node, int depth) {
        result = depth > result ? depth : result; // 中

        if (node->left == NULL && node->right == NULL) return ;

        if (node->left) { // 左
            depth++;    // 深度+1
            getDepth(node->left, depth);
            depth--;    // 回溯，深度-1
        }
        if (node->right) { // 右
            depth++;    // 深度+1
            getDepth(node->right, depth);
            depth--;    // 回溯，深度-1
        }
        return ;
    }
    int maxDepth(TreeNode* root) {
        result = 0;
        if (root == NULL) return result;
        getDepth(root, 1);
        return result;
    }
};
```
Time Complexity: O(n)

### 559. Maximum Depth of N-ary Tree

Link: [559. Maximum Depth of N-ary Tree](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/)

**Idea**

- similar to 104, but a N-ary tree which means each node can have any number of children
- use a for loop to iterate through all children, count for height,
- each function call marked as height 1,  so each return plus one i.e each recursive call adds 1 to the depth count to include the current node's level in the overall depth of the tree

**Solution**

``` ccp
// recursion
class Solution {
public:
    int maxDepth(Node* root) {
        if(root==NULL) return 0;
        int depth = 0;
        for(int i=0; i<root->children.size();i++){
            depth = max(depth,maxDepth(root->children[i]));
        }
        return depth+1;
    }
};

// BFS
class Solution {
public:
    int maxDepth(Node* root) {
        
        queue<Node*> que;
        if(root!=NULL) que.push(root);
        int depth = 0;

        while(!que.empty()){
            int size = que.size(); // in the following while loop, this size is changed because we add more nodes to the queu3
            depth++;     // log 
            for(int i = 0; i<size; i++){
                Node* node = que.front();
                que.pop();
                for(int j = 0; j < node->children.size();j++){
                    if(node->children[j]) que.push(node->children[j]);
                }
            }
        }
        return depth;
    }
};
```

### 111. Minimum Depth of Binary Tree
Link:[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)


**Idea**
- similar to max depth
- but need to handle if root's one child is null we have to go to another,
- because the null side will not lead us to the leaf node.
- in the context of binary tree, the root itself is not typically considered as a leaf node. 

**Solution**

```ccp
// recursion 
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == NULL) return 0;
        int left = minDepth(root->left);
        int right = minDepth(root->right);

        if(root->left == NULL || root->right ==NULL){
            return max(left,right)+1;
        }

        return min(left,right)+1;
    }
};

// BFS
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root ==NULL) return 0;
        queue<TreeNode*> que;
        que.push(root);
        int depth = 0;

        while(!que.empty()){
            int sz = que.size();
            depth++;
            for (int i = 0; i<sz; i++){
                TreeNode* node = que.front();
                que.pop();
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);

                if(!node->left && !node->right) return depth;
            }
        }
        return depth;
    }
};
```


### 222
Link:[222. Count Complete Tree Nodes
](https://leetcode.com/problems/count-complete-tree-nodes/description/)


**Idea**
- if it is a perfect binary tree, we just have to calculate it directly
- if not, we have to recursively call the function to count left nodes and right nodes

**Solution**

```ccp
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root == NULL) return 0;
        TreeNode* right = root->right;
        TreeNode* left = root->left;

        int r,l = 0;
        while(left){
            l++;
            left = left->left;
        }
        while(right){
            r++;
            right  = right->right;
        }

        if(l == r) return (2 << l )-1;

        return countNodes(root->left) + countNodes(root->right)+1;


    }
};

// recursion
class Solution {
public:
    int getNodesSum(TreeNode* cur){
        if(cur==0) return 0;
        int left = getNodesSum(cur->left);
        int right = getNodesSum(cur->right);
        int sum = left+right+1;
        return sum;
    }
    int countNodes(TreeNode* root) {
        return getNodesSum(root);

    }
};
```

