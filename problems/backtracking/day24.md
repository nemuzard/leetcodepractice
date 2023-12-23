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

