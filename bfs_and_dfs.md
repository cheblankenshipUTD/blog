## BFS and DFS

This is a note about Breadth First Search(BFS) and Depth First Search(DFS).

- Breadth First Search code (using queue)
- Depth First Search code (using recursive call stack)




Input and global scope vars

``` cpp
#define ROW 8
#define COL 8

// Adjacency Matrix
int A[ROW][COL] = {
    {0,0,0,0,0,0,0,0}, // empty
    {0,0,1,1,1,0,0,0}, // vertex 1
    {0,1,0,1,0,0,0,0}, // vertex 2
    {0,1,1,0,1,1,0,0}, // vertex 3
    {0,1,0,1,0,1,0,0}, // vertex 4
    {0,0,0,1,1,0,1,1}, // vertex 5
    {0,0,0,0,0,1,0,0}, // vertex 6
    {0,0,0,0,0,1,0,0}  // vertex 7
};

// Used for both BFS and DFS
int visited[ROW]= {0};

// Used for BFS
std::queue<int> Q;
```



### BFS

0. Input: Adjacency Matrix and vertex
1. Push the vertex into queue.
2. Loop while queue is not empty.
    2-a. Pop first element from queue.
    2-b. Print the vertex.
    2-c. Loop through the adjacent vertices and insert into queue and update visited array.

For Breadth First Search, I wrote a function that takes two inputs. Adjacency matrix (2D array) and starting vertex (integer). It uses a queue and array to handle the exploration. One array (or hash-table) will track the visited vertex so the function does not have to visit the same vertex again. Queue will help which order to visit. 

Code for BFS

``` cpp
void BFS(A[ROW][COL], int v)
{
    Q.psuh(v);
    while(!Q.empty())
    {
        int current = Q.first();
        Q.pop();
        printf("%d ", current);
        visited[current] = 1;
        
        for(int col = 1; col < COL; col++)
        {
            if(A[current][col] == 1 && visited[col] == 0)
            {
                Q.push(col);
                visited[col] = 1;
            }
        }
    }
}
```

### DFS

For Depth First Search, I used the recursive call stack to control the order of which vertex to visit. Similar to BFS, it uses an array to keep track of visited vertices. If statement will control the recursive call by checking if vertex was visited. 

Example

``` cpp

void DFS(A[ROW][COL], int v)
{
    if(visited[v] == 0)
    {
        pritnf("%d ", v);
        visited[v] = 1;
        for(int col = 1; col < COL; col++)
        {
            if(A[v][col] == 1 && visited[col] == 0)
            {
                DFS(A, col);
            }
        }
    }
}

```

