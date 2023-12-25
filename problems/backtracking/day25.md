### 216

**Idea**
- This problem is very similar to no 77. Combinations
- remember subtract when perform backtracking

**Solution**

```ccp
class Solution {
public:
    vector<int> path;
    vector<vector<int>> result;
    void backtracking(int n, int k, int startIndex,int count){
        if(path.size() == k){
            if(count==n) result.push_back(path);
            return;
        }

        for(int i = startIndex; i <= n; i++){
            path.push_back(i);
            count+=i;
            backtracking(n,k,i+1,count);
            count-=i;
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        result.clear();
        path.clear();
        backtracking(n,k,1,0);
        return result;
    }
};
```

### 17.

**Idea**



**Solution**

```ccp
class Solution {
private:
    const string letterMap[10]= {
        "",
        "",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz",
    };
public:
    string s;
    vector<string> result;
    void backtracking(const string& digits, int index){
        if(index == digits.size()){
            result.push_back(s);
            return;
        }
        // element of the input 
        int digit = digits[index] - '0';
        // respect to which letters 
        string str  =  letterMap[digit];

        for(int i = 0; i< str.size();i++){
            s.push_back(str[i]);
            // index + 1 : next input digit; if input is "23", this will point to '3'
            backtracking(digits,index+1);
            s.pop_back();
        }
    }

    vector<string> letterCombinations(string digits) {
        s.clear();
        result.clear();
        if(digits.size()==0) return result;
        backtracking(digits,0);
        return result;
    }
};
```
