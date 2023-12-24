### Backtracking Algorithm 
- Usually in recursion
- Brutal force search
- Problems can be solved with Backtracking algorithm:
- 1) Combinations - order does not matter 
  2) cutting problems
  3) subset problems
  4) chessboard problems
- All these problems can be abstract to certain tree structure, i.e n-ary tree
- width of the tree is the size of the problem instances (use for loop)
- depth is the depth of the recursion

```ccp
void backtracking(some parameters...){
  // stop condition
  if(stop condition){
    collect result;
    return;
  }
  // logic for single layer
  for(elements in the subset){
    process node;
    recursion;
    backtracking;
  }
  clear;
}
```


### 77.  Combinations
- brutal force, use for loop
- size of 2 then use 2 for loop, size of n , use n for loops,,
- Use backtracking
-  1. determine stop condition: if path.size == k, add path to result, and return
   2. single level logic: use for loop to search, and perform backtracking
   3. key is set i = startIndex in the for loop.

 **Solution**
 
```ccp
class Solution {
private:
    vector<int> path;
    vector<vector<int>> result;
    void backtracking(int n,int k,int startIndex){
        if(path.size()==k){
            result.push_back(path);
            return;
        }

        for(int i = startIndex;i<=n;i++){
            path.push_back(i);
            backtracking(n,k,i+1);
            path.pop_back();
        }

    }

public:
    vector<vector<int>> combine(int n, int k) {
        result.clear();
        path.clear();
        backtracking(n,k,1);
        return result;
    }
};
```

This is a brutal force algorithm! Time complexity is O(C(n,k))
