### 39. Combination Sum
Link: [ 39. Combination Sum](https://leetcode.com/problems/combination-sum/description/)

**Idea**
- Combination: order does not matter, so [1,2] and [2,1] are the same
- each for loop, we will not delete the current element in the original given set
- so we pass i in our recursive function calls



**Solution**

```ccp
class Solution {
public:
    vector<int> path;
    vector<vector<int>> result;
    int sum;
    void backtracking(vector<int>& candidates, int target, int sum,int index){
        if(sum == target){
            result.push_back(path);
            return;
        }

        for(int i = index; i < candidates.size();i++){
                
            if(sum+candidates[i]<=target){
                sum += candidates[i];
                path.push_back(candidates[i]);
                backtracking(candidates,target,sum,i);
                sum-=candidates[i];
                path.pop_back();
            }
            
            
        }
 

    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        if(candidates.empty()) return result;

        result.clear();
        path.clear();

        backtracking(candidates,target, 0,0);
        return result;
    }
};
```
