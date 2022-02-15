
## Leetcode: Remove Duplicates from Sorted List (83)
### Question

Given the  `head`  of a sorted linked list,  _delete all duplicates such that each element appears only once_. Return  _the linked list  **sorted**  as well_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/list1.jpg)

**Input:** head = [1,1,2]
**Output:** [1,2]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/list2.jpg)

**Input:** head = [1,1,2,3,3]
**Output:** [1,2,3]

**Constraints:**

-   The number of nodes in the list is in the range  `[0, 300]`.
-   `-100 <= Node.val <= 100`
-   The list is guaranteed to be  **sorted**  in ascending order.


#### Solution
I used fast & slow pointer approach to traverse/remove duplicated nodes from the linked-list. 

``` cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        
        ListNode* s = NULL;
        ListNode* f = NULL;
        
        // edge case #1 (empty ll)
        if(head == NULL)
        {
            return NULL;
        }
        
        // edge case #2 (only one node in ll)
        if(head != NULL && head->next == NULL)
        {
            return head;
        }
        
        
        // initialize f and s pointer
        s = head;
        f = head->next;
        
        // loop until fast ptr hits NULL
        while(f != NULL)
        {
            if(s->val == f->val)
            {
                ListNode* t = f;
                f = f->next;
                s->next = f;
                delete t;
            }
            else
            {
                s = f;
                f = f->next;
            }
        }
        
        return head;
    }
};
```