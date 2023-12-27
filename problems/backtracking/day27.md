### 39. Combination Sum
Link: [ 39. Combination Sum](https://leetcode.com/problems/combination-sum/description/)

**Idea**
- Combination: order does not matter, so [1,2] and [2,1] are the same
- each for loop, we will not delete the current element in the original given set, i.e, use the current index to show repeats
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

### 40, Combination sum and remove duplicates

**Idea**
- the key point is to remove duplicates at each level, not each path
- first we have to sort array, if the previous = current, we continue
- init a boolean array `used` to record and distinguish if it is used in path or level
- we set to true if it is used in its path, so we can know if it is false, then we are working on a certain layer,
- ` if(i>0 && candidates[i] == candidates[i-1] && used[i-1]==0 )continue;` that's why we check `used[i-1]==0` here

**Solution**

```ccp
class Solution {
public:
    vector<int> path;
    vector<vector<int>> result;
    void backtracking(vector<int>& candidates, int target, int sum, int index, vector<bool>& used){
        if(sum>target) return;
        if(sum==target){
            result.push_back(path);
            return;
        }

        for(int i = index; i < candidates.size();i++){
            // remove duplicates
            if(i>0 && candidates[i] == candidates[i-1] && used[i-1]==0 )continue;
            sum+=candidates[i];
            used[i]=true;
            path.push_back(candidates[i]);
            backtracking(candidates,target,sum,i+1, used);
            used[i] = false;
            sum-=candidates[i];
            path.pop_back();
            
        }
    }
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        if(candidates.empty()) return result;
        vector<bool> used(candidates.size(),0);
        result.clear();
        path.clear();
        sort(candidates.begin(),candidates.end());

        backtracking(candidates,target,0,0,used);
        return result;
        
    }
};
```


### 131. Palindrome Partitioning
Link: [131.Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)


**Idea**
- startIndex is the cutting point
- we have to check if it `isPalindrome`, if it is not we continue and if it is, we put the substring on `result`
- [startIndex, i] is the range of our subset.
- so when we perform backtracking, i should increase by 1, i.e pass i+1 to the recursive function

**Solution**

```ccp

```class Solution {
public:
    vector<string> path;
    vector<vector<string>> result;
    bool isPalindrome(const string& s, int start, int end){
        for(int i = start, j = end; i<j;i++,j--){
            if(s[i]!=s[j]) return false;
        }
        return true;
    }
    void backtracking(const string& s, int startIndex){
        // means we already found one partition becasue the last cutting line is after the last element
        if(startIndex>=s.size()){
            result.push_back(path);
            return;
        }

        for(int i = startIndex; i <s.size(); i++){
            if(isPalindrome(s,startIndex,i)){
                string str = s.substr(startIndex,i-startIndex+1);
                path.push_back(str);
            }else{
                continue;
            }
            backtracking(s,i+1);
            path.pop_back();
        }
    }
    vector<vector<string>> partition(string s) {
        result.clear();
        path.clear();
        backtracking(s,0);
        return result;
    }
};

Time Complexity: O(n*2**n)

