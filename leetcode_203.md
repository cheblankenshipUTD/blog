

## Leetcode: Remove Linked List Element (203)

### Question

Given the  `head`  of a linked list and an integer  `val`, remove all the nodes of the linked list that has  `Node.val == val`, and return  _the new head_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

**Input:** head = [1,2,6,3,4,5,6], val = 6
**Output:** [1,2,3,4,5]

**Example 2:**

**Input:** head = [], val = 1
**Output:** []

**Example 3:**

**Input:** head = [7,7,7,7], val = 7
**Output:** []

**Constraints:**

-   The number of nodes in the list is in the range  `[0, 104]`.
-   `1 <= Node.val <= 50`
-   `0 <= val <= 50`


#### Solution #1

For this problem, I used `two pointer` approach. One pointer at 'current', and another pointer pointed at 'previous' location. The time complexity is `O(n)`. The challege was to handle the edge case such as all nodes having the target value.

Submitted Code

``` cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {

        ListNode* p = NULL;
        ListNode* q = NULL;

        while(head != NULL && head->val == val)
        {
            head = head->next;
        }

        p = head;
        q = head;

        while(p != NULL)
        {
            if(p->val == val)
            {
                q->next = p->next;
                p = p->next;
            }
            else
            {
                q = p;
                p = p->next;
            }
        }

        return head;

    }
};
```
