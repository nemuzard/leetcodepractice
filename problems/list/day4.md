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
        // cannot return head, because if only one element, head is still unchanged 
        return dummy->next;

    }
};

```


**Time Complexity:** O(n)




#### 160. 
**Description**
Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return `null`.

**Idea**
1. use the longer list to iterate and find intersection
2. if no same node is found, return `NULL`

> List A: A1 --> A2 --> ... --> An \
List B: B1 --> B2 --> ... --> Bm

`if m>n --> swap length and reference` \
List A:  \
A1 → A2 → A3 → ... → An  \
         ^     \
         |     \
         curB  

List B: \
B1 → B2 → B3 → ... → Bm \
         ^                     \
         |             \
         curA                
         
then iterate through `listA` and if intersection is found then return it, otherwise, `NULL`

**Solution**
```ccp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {

        int lenA = 0;
        int lenB = 0;
        ListNode* curA = headA;
        ListNode* curB  = headB;
        while(curA){
            lenA++;
            curA = curA->next;
        }
        while(curB){
            lenB++;
            curB = curB->next;
        }

        curA = headA;
        curB = headB;

        if(lenB>lenA){
            swap(lenA,lenB);
            swap(curA,curB);
        }

        int difference = lenA - lenB;
        while(difference--){
            curA = curA->next;
        } 
        while(curA!=NULL){
            if(curA == curB){
                return curA;
            }
            curA = curA->next;
            curB = curB->next;
        }

        return NULL;
    }
};

```


**Time Complexity:** O(n+m)




#### 142. Linked List Cycle II
**Description**
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

[142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

**Idea**
1. check if there is a cycle, use two pointers, one fast(move 2 steps) and a slow which moves one step;
2. if there is a cycle, they must meet each other at some point.
3. if there is no cycle, fast will pointer to `null`
4. after making sure there is a cycle, we check for index
5. initialize index1 and index2,  let index1 = fast, index2 = head
6. the position they met is the entrance of the cycle

**Solution**

```ccp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;

        while(fast && fast->next){
            fast = fast->next->next;
            slow = slow->next;
            // if they meet, then there is a cycle
            if(slow == fast){
                ListNode* index1 = fast;
                ListNode* index2 = head;

                while(index1!=index2){
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index2;
            }
            
        }
        return NULL; 
    }
};
```


**Time Complexity:**O(n)


