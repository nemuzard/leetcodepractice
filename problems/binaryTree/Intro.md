## Binary Tree
**Definition**
```ccp
struct TreeNode {
  int val;
  TreeNode* left;
  TreeNode* right;
  TreeNode(int x): val(x), left(NULL), right(NULL) {}
};

```
### Types
Full Binary Tree
1. Number of nodes = k**2 - 1, where k = depth
2. Every node has either 0 or 2 children but not 1 child.
3. Every level of the tree is completely filled, except for the last level
4. from left to right 

Complete Binary Tree
1. Every level is _completely filled_, except for the last level (left to right)
2. Often used in binary heap data structure
3. A _full binary tree_ must also a complete binary tree

Binary Search Tree
1. Time complexity of searching a specific node is log n
2. all left nodes < mid <= all right nodes, and each left and right subtree also satisfy this rule

Balanced Binary Search Tree/ Adelson-Velsky and Landis Tree(AVL)
1. Good for search
2. Either an empty tree or the absolute difference of the height of its left and right subtrees not greater than 1
3. Both left and right subtrees are also balanced
4. In cpp, `map`, `set`, `multimap`, `multiset` are implemented by balanced search tree --> so the time complexity of add and remove is log N \
_（Note: `unordered_set`, `unordered_map`, `unordered_set` use hash map）_
```ccp
       a    
    /     \
   b       c
 /  \     /  \
d    e   f    g

Array: [a,b,c,d,e,f,g]
```
> if the index of the parent node is i, then its left child is `i*2+1` and right child is `i*2+2`

[Breadth-First Traversal](https://www.youtube.com/watch?v=oDqjPvD54Ss)
- Use queue structure
- Level order traversal (iterative approach)
- O(V+E)
- Useful for finding the shortest path on unweighted graphs
- Two categories: `visited` and `not visited`
- starts at some arbitrary node and explores the neighbor nodes first, before moving to the next level neighbors
  
Depth-First Traversal 
- use stack/or recursion data structure (iterative/recursive)
- Preorder Traversal: Mid - left - right
- Inorder Traversal: left - mid - right
- Postorder Traversal: left - right - mid

Key Points for Recursion
1. define parameters and return value
```ccp
void traversal(TreeNode* cur, vector<int>& vec)
```
2. define stop condition
```ccp
if (cur == NULL) return;
```
3. determine the logic of the single level
```ccp
//example for preorder
vec.push_back(cur->val);    // right 
traversal(cur->left, vec);  // left 
traversal(cur->right, vec); // right 
```

Full code:
```ccp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void traversal(TreeNode* cur, vector<int>& vec){
        if(cur==NULL) return;
        vec.push_back(cur->val);
        traversal(cur->left, vec);
        traversal(cur->right,vec);
    }
    
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root,result);
        return result;
    }
    
};
```

Today's problem: 144, 145, 94
