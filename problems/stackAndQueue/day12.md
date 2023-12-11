### Slidingg Window && Top K Frequent Element
#### Sliding Window
**Description**

You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. 

You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

[239.Sliding Window Max](https://leetcode.com/problems/sliding-window-maximum/)

**Idea**
1. create a deque: _**always let the front be the current k max**_
2. if nums[i] is greater than nums[deque.back()], pop deque back, becasue we do not need small val
3. after pop all smalls, now the only biggest left in this k-elements, add i to deque, and then add nums[i] to our result vector
4. The reason of why we do not add nums[i] to result without adding i to deque is we want to keep track of current max index of the input vector(nums).
5. if `i - k == deque.front()`, means we _already finished finding the biggest of the current group of k element_, so we pop front


**Solution**
```ccp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {

        // dq stores references
        std::deque<int> dq;

        vector<int> res;
        

        for(int i=0;i<k;i++){
            //keep the first element in the deque is the current max
            while(!dq.empty() && nums[i]>nums[dq.back()]){
                dq.pop_back();               
            }
            //stores the references from back 
            dq.push_back(i);                      
        }
        //dq.front stores the reference of current max, becasue we pop back all val
        res.push_back(nums[dq.front()]);

        for(int i = k; i<nums.size();i++){
            // if i=k=dq.front, then means we have to find next k numbers. we already the previous k and found the greatest val starts at dq.front 
            if(i-k==dq.front()){
                dq.pop_front();
            }
            // keep front is the biggest
            while(!dq.empty() && nums[i]>=nums[dq.back()]){
                dq.pop_back();
            }
            dq.push_back(i);
            res.push_back(nums[dq.front()]);
        }
        return res;
    }
};
```
Time Complexity:O(n)

#### 347. Top K frequent element 
**Description**
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

[Top K frequent element ](https://leetcode.com/problems/top-k-frequent-elements/) 

Example 1:

>Input: nums = [1,1,1,2,2,3], k = 2 \
Output: [1,2]


Example 2:

>Input: nums = [1], k = 1 \
Output: [1]
 

Constraints:

> 1 <= nums.length <= 105 \
-104 <= nums[i] <= 104 \
k is in the range [1, the number of unique elements in the array]. \
It is guaranteed that the answer is unique

**Idea**
1. use `map` to store val and its occurence
2. sort the `map` according to its occurence in descending order
3. add first k element of the map to our result and return it by using `min_heap`, why not max_heap? --> because when pop the element, it will pop the greatest element which is the root of the heap and min heap wil pop the smallest 

**Solution**
```ccp

```


Time Complexity: 
