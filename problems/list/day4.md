### Linked List 
#### 24. Swap Nodes in Pairs
**Description**
Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

Example 1:
> Input: head = [1,2,3,4] \
Output: [2,1,4,3]

[24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

**Idea**
1. create a dummy: dummy(0) --> head(1) --> head.next (2)
2. Let dummy(0) --> head.next(2), head.next(2) --> head(1), head(1) --> head.next.next(3)
3. we need to know the previous node, so created a dummy head.
4. Need let cur == dummy, i.e. the node before two nodes which are being swapped
5. so if want to swap 3 and 4, cur should be at 2
6. when doing while loop, cannot flip the order of condition 
**Solution**
```ccp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {

        if(!head||!head->next){
            return head;

        }
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;

        while(cur->next && cur->next->next){
            // save 1
            ListNode* first = cur->next;
            // save 3
            ListNode* third= cur->next->next->next;
        
            // dummy's pointer points to 2
            cur->next = first->next;
            // 2 --> 1/temp
            cur->next->next = first;
            // 1-->3
            first->next = third;       

            cur = cur->next->next;
        }
        return dummy->next;
        
    }
};

```
**Always remember to save the reference**
**Time Complexity:** O(n)



#### 19.
**Description**


**Idea**


**Solution**
```ccp


```


**Time Complexity:**




#### 160. 
**Description**


**Idea**


**Solution**
```ccp


```


**Time Complexity:**




#### 142. 
**Description**


**Idea**


**Solution**
'''ccp


'''


**Time Complexity:**


