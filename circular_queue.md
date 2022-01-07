
## Create Circular-Queue using array
### Description
This is a source code of Circular-Queue class using array. Without implementing with a circular design, there is a chance of two pointers (front, rear) get stuck at the last index of an array which causes the queue be "full". Implemeting a circular indexing function will solve this problem.


**Code**


``` cpp
#include <limits.h> // INT_MIN
#include <stdlib.h> // malloc()
#include <stdio.h>  // printf()


class CircularQueue
{
private:
    int front;
    int rear;
    int size;
    int* Q;
public:
    CircularQueue();
    CircularQueue(int size);
    ~CircularQueue();
    void enqueue(int newData);
    int dequeue();
    int circularIndex(int rawIndex);
    bool isEmpty();
    bool isFull();
    void display();
};

CircularQueue::CircularQueue()
{
    this->front = 0;
    this->rear = 0;
}

CircularQueue::CircularQueue(int size)
{
    this->front = 0;
    this->rear = 0;
    this->size = size;
    this->Q = (int*)malloc(size * sizeof(int));
}

CircularQueue::~CircularQueue()
{
    free(this->Q);
}

void CircularQueue::enqueue(int newData)
{   
    printf("Enqueue ");
    if (isFull())
    {
        printf("Queue is full.\n");
        return;
    }
    this->rear = (this->rear + 1) % this->size;
    this->Q[this->rear] = newData;
    display();
}

int CircularQueue::dequeue()
{
    printf("Dequeue ");
    int x = INT_MIN;
    if (isEmpty())
    {
        printf("Queue is empty.\n");
        return x; // return -1 if dequeue did not happen
    }
    else
    {
        this->front = circularIndex(this->front);
        x = this->Q[this->front];
        display();
    }
    return x;
}

int CircularQueue::circularIndex(int rawIndex)
{
    return (rawIndex + 1) % this->size;
}

bool CircularQueue::isEmpty()
{
    if (this->front == this->rear)
    {
        return true;
    }
    return false;
}

bool CircularQueue::isFull()
{
    if ((this->rear + 1) % this->size == this->front)
    {
        return true;
    }
    return false;
}

void CircularQueue::display()
{
    if (isEmpty())
        return;
    
    // 
    int index = (this->front + 1) % this->size;
    do
    {
        printf("%d ", this->Q[index]);
        index = (index + 1) % this->size;
    } while (index != (this->rear + 1) % this->size);
    printf("\n");
}


int main(int argc, char const *argv[])
{

    CircularQueue* cq = new CircularQueue(5);

    //
    cq->enqueue(4);
    cq->enqueue(2);
    cq->enqueue(3);
    cq->enqueue(8);
    cq->enqueue(0);
    
    cq->dequeue();
    cq->dequeue();
    cq->dequeue();
    cq->dequeue();
    cq->dequeue();

    return 0;
}
```
