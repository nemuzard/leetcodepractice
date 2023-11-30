### Binary Search and Remove Element
#### 704. Binary Search
##### Problem Description 
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search `target` in nums. If `target` exists, then return its index. Otherwise, return -1.
You must write an algorithm with *O(log n)* runtime complexity.

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9

Output: 4

Explanation: 9 exists in nums and its index is 4

Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2

Output: -1

Explanation: 2 does not exist in nums so return -1

Link: [704. Binary Search](https://leetcode.com/problems/binary-search/description/)

##### Solution 
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;

        while(left<=right){
            int m = (left+right)/2;
            if(nums[m]>target){
                right = m - 1;
            }else if(nums[m]<target){
                left = m+1;
            }else{
                return m; 
            }
        }

        return -1;
    }
};
```
1. Divide an array into two parts
2. Left < mid < Right
3. If our target is on the left side of `mid`, then we search left; else search right (`if target != nums[mid]`)
4. if we search left, update right `right = mid - 1`
5. if we search right, update left `left = mid + 1`
6. update `mid`, `mid = (left+right)/2`
7. if nothing is found, return -1
Time Complexity: O(logn)
#### 27. Remove Element
##### Problem Description 
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be `k`, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return `k`.
##### Solution 
```ccp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow = 0;
        for(int fast = 0;fast < nums.size();fast++){
            if(nums[fast]!=val){
                nums[slow++]=nums[fast];
            }
        }
        return slow;
    }
};
```
1. Use two needles, one is `fast` and another one is `slow`, and both of them init to 0
2. Use `fast` to traverse the entire array
3. If found `val` which is the num we want to remove, we do nothing (`fast++`)
4. If `nums[fast]!=val`, means we can keep this element --> `nums[slow++] = val`
5. Return `slow` which is equal to the number of elements
Time Complexity: O(n)
