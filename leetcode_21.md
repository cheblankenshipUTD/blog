
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

#### Solution 1 (iterative approach & in-place manipulation)


``` cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2)
    {
        
        if(!list1 && !list2) return NULL;
        if(!list1) return list2;
        if(!list2) return list1;
        
        ListNode* newH = (list1->val < list2->val) ? list1 : list2;
        
        while(list1 != NULL && list2 != NULL)
        {
            
            if(list1->val < list2->val)
            {
                while(list1 && list1->next && list1->next->val < list2->val)
                    list1 = list1->next;
                ListNode* temp = list1->next;
                list1->next = list2;
                list1 = temp;
            }
            else
            {
                while(list2 && list2->next && list2->next->val <= list1->val)
                    list2 = list2->next;
                ListNode* temp = list2->next;
                list2->next = list1;
                list2 = temp;
            }
        }
        
        return newH;
        
    }
};
```


#### Solution 2 (recursive approach)


``` cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* p1, ListNode* p2)
    {
        
        if(p1 == NULL && p2 == NULL) return NULL;
        return helper(p1, p2);
    }
    
    ListNode* helper(ListNode* p1, ListNode* p2)
    {
        // base
        if(p1 == NULL) return p2;
        if(p2 == NULL) return p1;
        
        // recursive
        ListNode* temp = NULL;
        if (p1->val < p2->val)
        {
            temp = p1;
            temp->next = helper(p1->next, p2);
            return temp;
        }
        temp = p2;
        temp->next = helper(p1, p2->next);
        return temp;
    }
    
};
```