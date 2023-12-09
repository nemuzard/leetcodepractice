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
There are 3 basic cases: \
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
Time Complexity: O(n)
#### 1047.
**Description**
You are given a string s consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them. \
We repeatedly make duplicate removals on s until we no longer can. \
Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

 

Example 1:

> Input: s = "abbaca" \
Output: "ca"

Explanation: \
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".

Example 2:

> Input: s = "azxxzy" \
Output: "ay"

Problem Link: [1047. Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
**Idea**
1. Implement a stack to store each char,
2. When encounter the same char, pop the stack!
3. becasue stack is *LIFO*, so we have to reverse to return 
##### Solution:
```ccp
class Solution {
public:
    string removeDuplicates(string s) {
        stack<char> ch;

        for(char c : s){
            if( !ch.empty() && ch.top()==c ){
                ch.pop();
            }else{
                ch.push(c);
            }
            
        }

        string res = "";
        while(!ch.empty()){
            res+=ch.top();
            ch.pop();
        }
        reverse(res.begin(),res.end());
        return res;

        
    }
};
```
Time Complexity: O(n)

#### 150. Evaluate Reverse Polish Notation
**Description**
You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are '+', '-', '*', and '/'. \
Each operand may be an integer or another expression. \
The division between two integers always truncates toward zero. \
There will not be any division by zero. \
The input represents a valid arithmetic expression in a reverse polish notation. \
The answer and all the intermediate calculations can be represented in a 32-bit integer. \
 

Example 1:

> Input: tokens = ["2","1","+","3","*"] \
Output: 9 \
Explanation: ((2 + 1) * 3) = 9

Example 2:

> Input: tokens = ["4","13","5","/","+"] \
Output: 6 \
Explanation: (4 + (13 / 5)) = 6

Example 3:

> Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"] \
Output: 22 \
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5 \
= ((10 * (6 / (12 * -11))) + 17) + 5 \
= ((10 * (6 / -132)) + 17) + 5 \
= ((10 * 0) + 17) + 5 \
= (0 + 17) + 5  \ 
= 17 + 5 \
= 22

Problem Link: [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

**Idea**
1. Similar to remove duplicates,
2. we init an empty stack `sk`
3. if `tokens[i] == some opr`, then we pop two nums in our stack, and according rule, we num2 opr num1
4. we push the result to our stack `sk`
5. We do not consider *invalid testcase*
##### Solution:
```ccp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<long long > sk;
        for(int i = 0;i<tokens.size();i++){
            if(tokens[i]=="+" ||tokens[i]=="-" ||tokens[i]=="*" ||tokens[i]=="/" ){
                
                long long num1 = sk.top();
                sk.pop();
                long long num2 = sk.top();
                sk.pop();
                

                if(tokens[i]=="+") sk.push(num1+num2);
                if(tokens[i]=="-") sk.push(num2-num1);
                if(tokens[i]=="*" ) sk.push(num2*num1);
                if(tokens[i]=="/") sk.push(num2/num1);
            }else{
                sk.push(stoll(tokens[i]));
            }
        }
        int res = sk.top();
        sk.pop();
        return res;
    }
};
```
Time Complexity: O(n)
