### Day2: Square of a Sorted Array, 
#### Square of a Sorted Array
##### Description 
Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example 1:

> Input: nums = [-4,-1,0,3,10] \
> Output: [0,1,9,16,100] \
> Explanation: After squaring, the array becomes [16,1,0,9,100]. \
> After sorting, it becomes [0,1,9,16,100]. 

Example 2: 
> Input: nums = [-7,-3,2,3,11] \
> Output: [4,9,9,49,121] 

Link: [Problem 977. Square of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)

Solution
``` cpp
#include <vector>

class Solution {
public:
    std::vector<int> sortedSquares(std::vector<int>& nums) {
        int i = 0;
        int j = nums.size() - 1;
        int k = nums.size() - 1;
        std::vector<int> result(nums.size(), 0);

        while (i <= j) {
            if (nums[i] * nums[i] < nums[j] * nums[j]) {
                result[k--] = nums[j] * nums[j];
                j--;
            } else {
                result[k--] = nums[i] * nums[i];
                i++;
            }
        }

        return result;
    }
};

```
1. this is a double-pointer solution
2. i is the front pointer and j is the back pointer
3. we will add squared elements **from bigger to smaller/from back to front**, and k is the initial index
4. while i and j have not met, we compare squared values and **add bigger** one to **result vector**
5. after each comparison, we have to either increment i/decrement k or decrement both k and j.
**Time Complexity: O(n)**

#### Minimum Size Subarray Sum
##### Description 
Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

Example 1:

> Input: target = 7, nums = [2,3,1,2,4,3] \
Output: 2 \
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

Example 2:

>Input: target = 4, nums = [1,4,4] \
Output: 1 


Example 3: 

> Input: target = 11, nums = [1,1,1,1,1,1,1,1] \
Output: 0
Link: [209.Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
##### Solution 
```ccp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int result = INT_MAX;
        int subL = 0;
        int sum = 0;
        int i = 0;
        for(int j = 0; j < nums.size(); j++){
            sum+=nums[j];
            while(sum>=target){
                subL = j-i+1;
                result = min(subL,result);
                sum = sum - nums[i];
                i++; 
            }
        }
        return min(result,subL);
    }
};
```
1. Sliding window
2. initialize the result to the max, and we iterate through the array and add up elements until the sum is greater than the traget
3. while target < sum, update length of subarray `j-i+1`, and then we subtract `nums[i]`
4. select a smaller length as our result  
Time Complexity: O(n)
#### 59. Spiral Matrix II
##### Description 
Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order. \
Example 1:
> Input n = 3 \
> Output = [[1,2,3],[8,9,4],[7,6,5]]

##### Solution 
``` ccp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
    
    std::vector<std::vector<int>> matrix(n, std::vector<int>(n, 0));
    int startx = 0;
    int starty = 0;

    int count = 1;
    int loop_count = 0;

    while(loop_count < n/2 ){
        // Top 
        for(int j = starty; j<n-loop_count-1;++j){
            matrix[startx][j] = count ++;
        }

        // right 
        for (int i = startx; i <n - loop_count-1;++i){
            matrix[i][n-loop_count-1] = count++;
        }


        // bottom
        for(int j = n -loop_count-1; j >starty; --j ){
            matrix[n-loop_count-1][j] = count++;
        }

        // left
        for (int i = n-loop_count-1;i>startx;--i){
            matrix[i][starty] = count++;
        }
        ++starty;
        ++startx;
    }

    if(n%2!=0){
        matrix[n/2][n/2] =  count;
    }
    return matrix;

    }
};
```
1. we will not count the last element,
2. we draw 'circles' from 1 to n
3. We will have to update starting point of x and y after loops
Time Complexity:O(n**2)
