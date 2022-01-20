## Leetcode: Palindrome Linked List (234)
### Question

Given the head of a singly linked list, return true if it is a palindrome.

Example 1:
Input: head = [1,2,2,1]
Output: true


Example 2:
Input: head = [1,2]
Output: false

Constraints:
The number of nodes in the list is in the range [1, 105].
0 <= Node.val <= 9



#### Solution #1
I followed the abstract steps below to implement the solution in C++.
1. Declare slow/fast pointer then initialize them eql to head address. O(1)

2. Iterate through the linked list from head using the two pointers (moving slow ptr by one and fast ptr by two positions). Stop when fast pointer hits NULL. O(n)

3. Slow pointer will be standing at middle position.

4. Call "revere lisnked list" function by passing slow pointer as a argument. O(n)

5. Iterate from slow pointer address until NULL (check linkedList[head++] != linkedList[slow++]). O(n)

6. If inEquality is not found, return true. If the link list is not palindrome, it will return false at step 5.


Submitted Code

``` cpp

class Solution {
public:

    ListNode* reverse(ListNode* ptr)
    {

        if(ptr == NULL)
        {
            return NULL;
        }

        if(ptr->next == NULL)
        {
            return ptr;
        }



        ListNode* fast = ptr->next;
        ListNode* curr = ptr;
        ListNode* prev = NULL;

        while(fast != NULL)
        {
            curr->next = prev;
            prev = curr;
            curr = fast;
            fast = fast->next;
        }

        curr->next = prev;


        return curr;

    }


    bool isPalindrome(ListNode* head)
    {

        if(head == NULL || head->next == NULL)
        {
            return true;
        }

        //1 iterate through the link list using fast/slow ptrs
        ListNode* f = head;
        ListNode* s = head;
        while(f != NULL && f->next != NULL)
        {
            s = s->next;
            f = f->next->next;
        }

        //2 reverse linked list from the slow ptr
        ListNode* re = reverse(s);    

        //3 delcare/initialize temp ptr
        ListNode* temp = head;

        //4 compare val btwn original and reveresed
        while(re != NULL)
        {
            if(re->val != temp->val)
            {
                return false;
            }
            re = re->next;
            temp = temp->next;
        }

        //5 return true if it doesn't hit the cases in 4
        return true;

    }
};

```
