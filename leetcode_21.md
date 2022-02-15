
## Leetcode: Merge Two Sorted Lists (21)
### Question

You are given the heads of two sorted linked lists  `list1`  and  `list2`.

Merge the two lists in a one  **sorted**  list. The list should be made by splicing together the nodes of the first two lists.

Return  _the head of the merged linked list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** list1 = [1,2,4], list2 = [1,3,4]
**Output:** [1,1,2,3,4,4]

**Example 2:**

**Input:** list1 = [], list2 = []
**Output:** []

**Example 3:**

**Input:** list1 = [], list2 = [0]
**Output:** [0]

**Constraints:**

-   The number of nodes in both lists is in the range  `[0, 50]`.
-   `-100 <= Node.val <= 100`
-   Both  `list1`  and  `list2`  are sorted in  **non-decreasing**  order.

#### Solution #1
I declared/initialized an empty linked-list that will hold the two merged linked list. In addition, I initialized head pointer variable for returning purpose. Since the two linked lists are sorted, the while loop can iterate through them using pointers until one of the linked list reaches a null. After one of the linked-list reaches NULL, I just have to insert the left over nodes into the merged linked list.

``` cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        
        // edge case
        if(list1 == NULL && list2 == NULL)
        {
            return NULL;
        }
        
        // 
        if(list1 != NULL && list2 == NULL)
        {
            return list1;
        }
        
        if(list1 == NULL && list2 != NULL)
        {
            return list2;
        }
        
        // Declare empty merged linked list 
        ListNode* ml = NULL;
        ListNode* mh = NULL;
        
        // loop through two sorted ll
        while(list1 != NULL && list2 != NULL)
        {
            // list1 node is smaller than list2 node
            if(list1->val <= list2->val)
            {
                // insert list1 node into merged ll
                if(ml == NULL)
                {
                    ml = list1;
                    mh = list1;
                    list1 = list1->next;
                }
                else
                {
                    ml->next = list1;
                    ml = ml->next;
                    list1 = list1->next;
                }
            }
            else
            {
                // insert list1 node into merged ll
                if(ml == NULL)
                {
                    ml = list2;
                    mh = list2;
                    list2 = list2->next;
                }
                else
                {
                    ml->next = list2;
                    ml = ml->next;
                    list2 = list2->next;
                }
            }
        }
        
        // insert left over nodes
        if(list1 != NULL || list2 == NULL)
        {
            while(list1 != NULL)
            {
                ml->next = list1;
                ml = ml->next;
                list1 = list1->next;
            }
        }
        else
        {
            while(list2 != NULL)
            {
                ml->next = list2;
                ml = ml->next;
                list2 = list2->next;
            }
        }
        
        return mh;
        
    }
};
```