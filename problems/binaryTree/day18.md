### 513 Find bottom left tree value
Link:[513 Find bottom left tree value](https://leetcode.com/problems/find-bottom-left-tree-value/description/)

**Idea**
- BFS
  - the idea of BFS is the element at each index of the queue, it represents the `parent node`,
  - inside the for loop, we add the previous parent's children as new roots to perform BFS  
  - In this problem, the left is at index 0

- Recursion / preorder traversal
  - Three steps of recursion:
    -  determine parameters and return
      -  `maxDepth = INT_MIN` to record the max depth
      - `result` to store the leftmost value at the lowest level of the tree
      - `void traversal(int maxDepth, TreeNode* root)`
    -  determine stop condition(s)
      - when we encounter the leaf node, we should check the depth.
      - if the current depth is greater than our recorded maxDepth, we update maxDepth and save the leftmost value
      -  the condition of the leftmost leaf --> check at the parent's level --> `root->`  
    -  determine single-level logic
    
**Solution**

```ccp
// BFS
class Solution {
public:
    int findBottomLeftValue(TreeNode* root) {
        if(root==NULL) return 0;                    //

        queue<TreeNode*> que;                       //
        que.push(root);                             //
        int result = 0;                             //
        while(!que.empty()){                       //   BFS loop
            int size = que.size();                  //
            for(int i = 0; i<size; i++){            //
                TreeNode* node = que.front();       //
                que.pop();                          //
                if(i==0) result = node->val; // last line first node, specific problem condition 
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
                
            }
        }

        return result;
    }
};

// Preorder recursion
class Solution {
public:
    int maxDepth = INT_MIN;
    int result;
    void traversal(int depth, TreeNode* root){
        // key point is we always check left first thus always return left first!
        if(root->left == NULL && root->right==NULL){
            if(maxDepth<depth){
                maxDepth=depth;
                result = root->val;
            }

            return;
        }
        if(root->left){
            depth++;
            traversal(depth,root->left);
            depth--; // this is for return to the previous level and check for the right side 
        }

        if(root->right){
            depth++;
            traversal(depth,root->right);
            depth--;
        }
        
    }
    int findBottomLeftValue(TreeNode* root) {
        if(root == NULL) return 0;
        traversal(0,root);
        return result;
    }
};
```

Time Complexity: O(n)


### 112 & 113
Link:[]()

**Idea**


**Solution**

```ccp
// 112 my solution
class Solution {
public:
    bool sum(TreeNode* cur, int s,int targetSum){

        if(cur == NULL) return false;
        s += cur->val;
        if(cur->left == NULL && cur->right == NULL){
           return s == targetSum;
        }

        return sum(cur->left,s,targetSum) || sum(cur->right,s,targetSum);

    }
    bool hasPathSum(TreeNode* root, int targetSum) {
        //if(root==NULL) return false;
        return sum(root,0,targetSum);
    }
};

// back

```

Time Complexity: O()



### 106 & 105
Link:[]()

**Idea**


**Solution**

```ccp

```

Time Complexity: O()

