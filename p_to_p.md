## Pointer to pointer

This is a note about pointer to pointer and other ways of passing variables to the function. Since I use Python frequently,
I had to review the C++ rules for function parameters and arguments.

- Pass by reference
- Pass by pointer
- Pass by pointer-to-pointer

### Pass by reference
When a variable is passed by reference, the argument will have the address of it's variable.
The argument will technically be a different name version of the passed variable.
It can be modify.

Example

``` cpp
void updateNumber(int &n)
{
    n = 100;
}

int main(int argc, char const *argv[])
{
    int x = 4;

    printf("x is %d. \n", x);
    updateNumber(x);
    printf("x is %d. \n", x);

    return 0;
}

```

Output

``` bash
x is 4.
x is 100.

```

### Pass by pointer
This is used commonly when passing a array. In C++, when you pass an array in argument, you can see by checking the size.
You won't get the whole array size. Only the size of the initial element size.
You can access/modify the array by index. Array has consistant memory size for each element; hence, it can move to the
correct index location.

Example

``` cpp

void fun(int A[], int size)
{
    printf("\nSize of element: %lu", sizeof(A));
    printf("\nSize argument: %d", size);
    printf("\nAddress of A: %p", &A[0]);
    printf("\nAddress of A[0]: %p", &A[0]);
    printf("\nAddress of i=1, A[i]=A[0]+(element size * i): %p", &A[1]);
    printf("\nAddress of i=2, A[i]=A[0]+(element size * i): %p", &A[2]);
    printf("\nAddress increasing by 4);
}

int main(int argc, char const *argv[])
{
    int array[4] = {3,9,23,65};
    int size = sizeof(array)/sizeof(array[0]);
    fun(array, size);
    return 0;
}

```


Output

``` bash
Size of element: 8
Size argument: 4
Address of A: 0x16d633400
Address of A[0]: 0x16d633400
Address of i=1, A[i]=A[0]+(element size * i): 0x16d633404
Address of i=2, A[i]=A[0]+(element size * i): 0x16d633408
Address increasing by 4

```

### Pass by pointer-to-pointer
First time I faced using this method was during developing a singly linked list.
For functions such as Insert(), or Delete(), I had to update the head pointer address.
Before knowing pointer-to-pointer, I was passing the head pointer as a pointer. This is technically passed
as a value; hence, it can read the address of what head is pointed to, however, function cannot modify the pointed address.
To allow head or other node pointer to be modify, it has to be passed by pointer-to-pointer.


Example

``` cpp
// Create linked list from array
void Create(int A[], int size, struct Node* head)
{
    struct Node* temp;
    struct Node* last;
    head->data = A[0];
    head->next = NULL;
    last = head;

    // create link list
    for (int i = 1; i < size; i++)
    {
        temp = new Node();
        temp->data = A[i];
        temp->next = NULL;
        last->next = temp;
        last = temp;
    }
}

void DisplayRec(struct Node* p)
{
    // Case 1: if head is initialized but not a linked list
    if (p != NULL && p->data == INT_MIN)
        return;

    // Case 2: check if node reached the tail
    if (p == NULL)
        return;

    printf("%d ", p->data);
    return DisplayRec(p->next);
}

// p: head pointer
// data: new node data
// position: insert to tail if position is not specified
void Insert(struct Node** p, int data, int position)
{
    struct Node* tail = NULL;
    struct Node* newNode = new Node(data);

    // Case 1: insert in head
    if (position == 0 || position == INT_MIN)
    {
        newNode->next = *p;
        *p = newNode;
        return;
    }

    // Case 2: insert after nth node
    tail = *p;
    for (int i = 1; i < position; i++)
    {
        if (tail->next == NULL)
        {
            printf("Out of range. Inserting to tail.\n");
            tail->next = newNode;
            return;
        }
        tail = tail->next;
    }
    newNode->next = tail->next;
    tail->next = newNode;
}

void Delete(struct Node** head, int target)
{
    // get the head address as a reference
    struct Node* current = *head;
    struct Node* tail = new Node();

    // delete head node
    if (current->data == target)
    {
        *head = current->next;
        free(current);
        return;
    }

    // iterate up to the node we want to delete
    while (current->next != NULL)
    {
        if (current->data == target)
        {
            tail->next = current->next;
            free(current);
            return;
        }
        // move tail ptr to current ptr node
        tail = current;
        // move current ptr to next ptr node
        current = current->next;
    }

    printf("Target not found.\n");

}



int main(int argc, char const *argv[])
{
    int A[] = {3, 5, 4, 7, 99};
    struct Node* head = new Node();

    // create
    Create(A, sizeof(A)/sizeof(A[0]), head);

    // display
    DisplayRec(head);

    // insert
    Insert(&head, 100, 0); // insert to head
    Insert(&head, 54, 2);  // insert after 2nd node
    // try inserting to out-of-range position. let it insert to tail
    Insert(&head, 32, 1000);

    Delete(&head, 100);
    printf("\n");
    DisplayRec(head);

    Delete(&head, 4);
    printf("\n");
    DisplayRec(head);

    return 0;
}

```


Output

``` bash
3 5 4 7 99 Out of range. Inserting to tail.
100 3 54 5 4 7 99 32
3 54 5 4 7 99 32
3 54 5 7 99 32

```
