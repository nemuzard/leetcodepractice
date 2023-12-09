### 203
[Problem: Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)
#### Solution
**Idea** 
1. We create a dummy head to unify the entire deleting process
2. cur is always set to be "the previous" node because when we are deleting, we will link the previous node of the target to the next node of the target. i.e we need the reference before the target node
3. **Do not forget to delete references**
``` ccp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        // create a dummy node and dummy->next = head
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode* cur = dummy;
        // we need know previous node and next node of our target node, so we define current as "the previous" node
        while(cur->next){
            if(cur->next->val == val){
                cur->next = cur->next->next;
            }else{
                cur = cur->next;
            }
        }

        ListNode* newHead = dummy->next;
        delete dummy;

        return newHead;
    }
};
```
Time Complexity: O(n)
### 707
[Problem 707: design linked list](https://leetcode.com/problems/design-linked-list/)
#### Solution
**Idea**
1. Create a dummy node for each operation! Dont ruin the entire list!
2. **Add at Index**: after checking if index is legal, when we start adding a new node, always set the current one step before. B/c we want to link nodes in this way `cur->new_node->cur->next`
3. **Delete at Index**: the same thing needs to be cautioned as add at index!
4. Remember increase/decrease the size of the linked list
``` ccp
class MyLinkedList {
public:
    ListNode* head;
    int size;
    MyLinkedList() {
        head = nullptr;
        size = 0;
    }
    
    int get(int index) {
        if(index>=size||index<0){
            return -1;
        }else{
            ListNode* dummy = new ListNode(-1);
            dummy->next = head;
            ListNode* cur = dummy->next;
            if(cur==nullptr){
                return -1;
            }
            while(index>0 && cur->next != nullptr){
                cur = cur->next;
                index--;
            }
            return cur->val;
        }
    }
    
    void addAtHead(int val) {
        ListNode* new_node = new ListNode(val);
        new_node->next = head;
        head = new_node;
        size++;    
    }
    
    void addAtTail(int val) {
        ListNode* new_node = new ListNode(val);
        if (!head) {
            head = new_node;
        }else{
            ListNode* cur = head;
            while (cur->next) {
                cur = cur->next;
            }
            cur->next = new_node;
        }
        size++;
    }
    
    void addAtIndex(int index, int val) {
        if(index>size){
            return;
        }
        if (index == 0){
            addAtHead(val);
            return;
        }

        ListNode* cur = head;
        // go to the index that is one step before our target
        // b/c we need the previous and the following nodes
        for(int i = 0; i <index-1;i++){
            if(cur == nullptr){
                return;
            }
            cur = cur->next;
        }

        ListNode* new_node = new ListNode(val);
        new_node->next = (cur ? cur->next : nullptr);
        if(cur){
            cur->next = new_node;
        }
        size++;
    }
    
    void deleteAtIndex(int index) {
        if (index < 0 || index >= size || head == nullptr) {
            return;
        }
        if(index == 0){
            ListNode* temp = head;
            head = head->next;
            delete temp;
            size --;
            return;
        }
        ListNode* cur = head;
        for(int i=0;i<index-1;i++){
            if(cur==nullptr||cur->next==nullptr){
                return;
            }
            cur = cur->next;
        }
        cur->next=(cur->next ? cur->next->next : nullptr);
        size --;

    }
};
```
Time Complexity: O(n)
### 206
**Idea**
__Double Pointer__
1. define pre and cur, cur init to `head` and pre is the `NULL` pointer
2. we will "flip" cur and pre, but need a `temp` to store `cur->next` before we actual flip pre and cur to make sure we are not losing reference
3. after flipped, we update cur to temp, which is `cur->next`
4. we should stop when `cur == NULL` and now, `pre` becomes our new head of the reversed list

__Recursion__
1. Similar to double pointer.
2. but recursively call `reverse` function to perform 'flip' and update `cur`
3. in this, `cur` becomes `temp` when call reverse function \
[206: reverse a list](https://leetcode.com/problems/reverse-linked-list/description/)
#### Solution
``` ccp
// Double Pointer
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = NULL; 
        ListNode* curr = head;
        ListNode* temp;

        while(curr){
            // store cur.next
            temp = curr->next;
            //reverse pointer
            curr->next = prev;
            prev = curr;
            // equ to move next
            // if curr == null, means we finish
            curr = temp;
        }
        
        return prev;

    }
};
```

Time Complexity: O(n)

``` ccp
//recursion
class Solution {
public:
    ListNode* reverse(ListNode* pre, ListNode* cur){
        if(cur == NULL) return pre;
        ListNode* temp = cur;
        cur->next = pre;

        return reverse(cur,temp);
    }
    ListNode* reverseList(ListNode* head) {
        

        return reverse(NULL,head);

    }
};
```
