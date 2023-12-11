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
        
            // set dummy's next node  ==  2
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
*A quick note*: why use dummy node? -- uniform the entire operation, so we dont have to check if the node is head


#### 19. Remove Nth Node From End of List
**Description**

[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
**Idea**
1. two pointers, one move ahead n steps and then move two pointers at the same time
2. then let fast move one additional steps in order to make slow points to the previous node of the target.


**Solution**
```ccp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        
        if(n<0){
            return head;
        }

        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* fast = dummy;
        ListNode* slow = dummy;

        while(n-- && fast!=NULL){
            fast = fast->next;
        }
        fast = fast->next;

        while(fast!=NULL){
            slow = slow->next;
            fast = fast->next;
        }
        slow->next = slow->next->next;
        // cannot return head, becasue if only one element, head is still unchanged 
        return dummy->next;

    }
};

```


**Time Complexity:** O(n)




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


