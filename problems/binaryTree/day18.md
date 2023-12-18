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
Link:[112 Path Sum](https://leetcode.com/problems/path-sum/) \
     [113 Path Sum 2](https://leetcode.com/problems/path-sum-ii/)

**Idea**
- pass targetSum as `count` to our function, each time we encounter a node, we minus the node val
- if it is the leaf node, and `count == 0`, means we have found the path, return true
  - if we are asking to return all paths that sum is equal to target
  - we have to init a path vector to store the node value, if it is leaf node, and count not equal to 0, we have to pop it, becasue it does not fullfill the requirement
  - then we go back and do the same procedure. 
- if not, we have to go back to the previous level, and make count = count + node val to stay unchanged
- if not find any path, we return false  

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

// backtrack
class Solution {
public:
    bool traversal(TreeNode* cur, int count){

        if(!cur->left && !cur->right && count == 0){
            return true;
        }
        if(!cur->left && !cur->right) return false;

        if(cur->left){
            count-=cur->left->val;
            if(traversal(cur->left,count)) return true;
            count+=cur->left->val;
        }


        if(cur->right){
            count -= cur->right->val;
            // dont need visit all nodes, as long as we find result, return
            if(traversal(cur->right, count)) return true;
            //not find, back to the previous level, and make count == previous count, i.e, backtrack 
            count+= cur->right->val;
        }

        return false;

    }
    bool hasPathSum(TreeNode* root, int targetSum) {
        if(root==NULL) return false;
        if(!root->left && !root->right && targetSum == root->val) return true;
        return traversal(root,targetSum-root->val);
    }
};
```


``` ccp
//113
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    // do not need return value because we are visiting the entire tree
    void traversal(TreeNode* cur, int count){
        if(!cur->left && !cur->right && count==0){
            result.push_back(path);
            return;
        }
        // sum not equal to target and will return to the point where we call the function recursively 
        if(!cur->left && !cur->right){
            return;
        }

        if(cur->left){
            path.push_back(cur->left->val);
            count -= cur->left->val;
            traversal(cur->left,count);
            // if arrives here, means we did not find result, and will continue 
            count+=cur->left->val;
            path.pop_back();
        }

        if(cur->right){
            path.push_back(cur->right->val);
            count -= cur->right->val;
            traversal(cur->right, count);
            // not found
            count+=cur->right->val;
            path.pop_back();
        }
        
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        result.clear();
        path.clear();
        if(root==NULL) return result;

        path.push_back(root->val);
        traversal(root,targetSum-root->val);
        return result;
    }
};


```

Time Complexity: O(n)

In the worst case of 112, still have to visit all nodes. 


### 106 & 105
Link:[]()

**Idea**


**Solution**

```ccp

```

Time Complexity: O()

