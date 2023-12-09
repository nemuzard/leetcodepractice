### Stack and Queue 2
#### 20. Valid Parentheses
**Description**
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. 

An input string is valid if: 
Open brackets must be closed by the same type of brackets. \
Open brackets must be closed in the correct order. \
Every close bracket has a corresponding open bracket of the same type. 

Example 1:
> Input: s = "()" \
> Output: true 

Example 2:
> Input: s = "(]" \
> Output: false

Problem Link: [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) \
**Idea**
There are 3 basic cases
1. {}()[] -- match
2. (( or )) -- not match 
3. {}(] -- not match

Implement a stack:
1. `sk.push(reversed_symbol)` if equal to `{([`
2. if `sk.empty()` --> no element equal to `{([`
3. if `sk.top() == string[i]` --> we found a match **Notice**: we must start with a open symbol, i.e. when we start to find matches/closed symbol, means we added all open symbols already, and the rule is we have to match symbols in order, otherwise is wrong. so the top of stack is equal to `string[i]` if there is a match ---> `sk.pop()`, else `return false`
**Notice**: should return `sk.empty()`, if sk is not empty, means we have extras. 


##### Solution:
```ccp
Input: string s 
stack<char> sk;
if(s.size()%2!=0) return false; // odd number must false
//start checking
for(int i = 0; i<s.size(); i++){
  if(s[i]=='('){
    ch.push(')');
  }else if(s[i]=='['){
    ch.push(']');
  }else if(s[i]=='{'){
    ch.push('}');
  }else if(ch.empty()||s[i]!=ch.top()){
    return false;
  }else if(s[i]==ch.top()){ // this is equivalent to else{..}
    ch.pop();
 }

}
return ch.empty();

```
Time Complexity: O()
#### 1047.
**Description**

Problem Link: []()
**Idea**

##### Solution:
```ccp

```
Time Complexity: O()

#### 150.
**Description**

Problem Link: []()
**Idea**

##### Solution:
```ccp

```
Time Complexity: O()
