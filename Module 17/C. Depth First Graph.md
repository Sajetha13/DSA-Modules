# Depth First Graph
## AIM:
To compose the code for the function createNode to traverse the graph below in the depth first fashion.

![image](https://github.com/user-attachments/assets/63552824-d0a3-49c6-a473-6db27d1f03e4)

## Algorithm
1. Start the program.
2. Create structures to store graph and nodes of the graph.
3. Allocate memory for a temporary structure to create a new node.
4. Store NULL in the next part of the temporary structure and the required vertex in the vertex part of it. Return temp.
5. End the program.

## Program:
```
#include <stdio.h>
#include <stdlib.h>

struct node {
  int vertex;
  struct node* next;
};

struct node* createNode(int v);

struct Graph {
  int numVertices;
  int* visited;

  // We need int** to store a two dimensional array.
  // Similary, we need struct node** to store an array of Linked lists
  struct node** adjLists;
};*/
struct node* createNode(int v) {
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->next=NULL;
    temp->vertex=v;
    return temp;
}

*/
```

## Output:

![image](https://github.com/user-attachments/assets/b336fd2a-767a-42c9-b9bc-760160dbfbf5)

## Result:
Thus, the C code for the function createNode to traverse the graph below in the depth first fashion is implemented successfully
