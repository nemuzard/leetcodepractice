### 530. Minimum Absolute Difference in BST
Link: [530. Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst/description/)

**Idea**
- use _inorder_ traversal and double pointers, one is `cur` and another is `pre`
- starts at searching left subtree, is cur == null, back to the previous level, set pre = cur
- then *starts right , but the leaf node does not have a right, so return again --> to the previous level, in this case, back to `cur = [2,1,3]`

**Solution**

```ccp
class Solution {
public:
int result = INT_MAX;
TreeNode* pre = NULL;

    void traversal(TreeNode* cur){
        if(cur == NULL) return;
        traversal(cur->left);
        if(pre!=NULL){
            result  = min(result,cur->val - pre->val);
        }

        pre=cur;
        traversal(cur->right);
    }
    int getMinimumDifference(TreeNode* root) {
        traversal(root);
        return result;
    }
};
```

### 501. Find Mode in Binary Search Tree
Link: [501. Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/description/)

**Idea**
- Key point is, set `current_count = 1` if  `cur->val != pre->val` since this is a Binary Search Tree
- if pre is not null and values are equal, we update  `current_count `
- compare  `current_count ` and  `max_count `, if they are equal, we push the value into our vector
- if  `current_count > max_count`, we clear the vector, then push the value. Because the most frequent value is the value of the current node.

**Solution**

```ccp
class Solution {
public:
int maxCount = 0;
int currentCount = 0;
vector<int> result;
TreeNode* pre = NULL;
    void traversal(TreeNode* cur){
        
        if(cur==NULL) return;
        traversal(cur->left);
    
        if(pre!=NULL && pre->val == cur->val){
            currentCount++;
        }else{
            currentCount = 1;
        }
    
        if(currentCount>maxCount){
            maxCount = currentCount;
            result.clear();
            result.push_back(cur->val);
        }else if(currentCount == maxCount){
            result.push_back(cur->val);
        }

        pre = cur;
        traversal(cur->right);


    }
    vector<int> findMode(TreeNode* root) {
        traversal(root);
        return result;
    }
};
```
