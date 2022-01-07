# Types of Recursion

In this blog I will like to go through examples of different recursions.

- Tail recursion
- Head recursion
- Tree recursion

## Tail Recursion
A recursion can be calssify as tail recursion when the last process beofre calling the function in call stack is it's own function.
Usually it's easy to convert tail recursion into loop. Some compilers will check if the recursion code can be convert into loop and reduce space complexity to O(1).

Example

``` cpp
void tailRec(int n)
{
    if(n > 0)
    {
        std::cout << n << std::endl;
        tailRec(n-1);
    }
}

int main(int argc, char const *argv[])
{
    tailRec(3);
    return 0;
}
```

Output

``` bash
3
2
1
```

## Head Recursion
A recursion can be calssify as head recursion when the logic has to process something during the resutning statement.
These recursion logic is not as easy to convert into loop.

Example

``` cpp
void headRec(int n)
{
    if(n > 0)
    {
        tailRec(n-1);
        std::cout << n << std::endl;
    }
}

int main(int argc, char const *argv[])
{
    headRec(3);
    return 0;
}
```

Output

``` bash
1
2
3
```

## Tree Recursion
You can classify a recursion as a tree recursion when it's recursion logic calls it's own twice or more times.
When you visualize the call stack, it looks like a tree. When it's calling two times in the recursion, then the call stack will look like a binary tree.

Example

``` cpp
void treeRec(int n)
{
    if(n > 0)
    {
        printf("%d \n", n); // step 1
        treeRec(n-1);       // step 2
        treeRec(n-1);       // step 3
    }
}

int main(int argc, char const *argv[])
{
    treeRec(3);
    return 0;
}
```

Output

``` bash
3
2
1
1
2
1
1
```
