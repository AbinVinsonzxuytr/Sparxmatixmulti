Abin Vinson 
s3 cse A

# Sparxmatixmulti


#include <stdio.h> #include <stdbool.h>

#define MAX_SIZE 100

struct Queue { int data[MAX_SIZE]; int priority[MAX_SIZE]; int front, rear; };

void initializeQueue(struct Queue *q) { q->front = -1; q->rear = -1; }

bool isFull(struct Queue *q) { return (q->rear == MAX_SIZE - 1); }

bool isEmpty(struct Queue *q) { return (q->front == -1); }

void enqueue(struct Queue *q, int item, int p) { if (isFull(q)) { printf("Queue is full. Cannot enqueue.\n"); return; }

int i;
for (i = q->rear; i >= 0; i--) {
    if (p > q->priority[i]) {
        q->data[i + 1] = q->data[i];
        q->priority[i + 1] = q->priority[i];
    } else {
        break;
    }
}

q->data[i + 1] = item;
q->priority[i + 1] = p;

if (q->front == -1) {
    q->front = 0;
}

q->rear++;
}

int dequeue(struct Queue *q) { if (isEmpty(q)) { printf("Queue is empty. Cannot dequeue.\n"); return -1; }

int item = q->data[q->front];
q->front++;

if (q->front > q->rear) {
    q->front = q->rear = -1;
}

return item;
}

int main() { struct Queue q; initializeQueue(&q);

enqueue(&q, 10, 2);
enqueue(&q, 20, 1);
enqueue(&q, 30, 3);
enqueue(&q, 40, 2);

printf("Dequeued item: %d\n", dequeue(&q));
printf("Dequeued item: %d\n", dequeue(&q));
printf("Dequeued item: %d\n", dequeue(&q));
printf("Dequeued item: %d\n", dequeue(&q));

return 0;
}
