
# Adjacency List Representation
## AIM:
To write a C program to represent the given graph using the adjacency list.

## Algorithm
1. Start the program.
2. Read the number of vertices and number of edges.
3. Read all edge pairs (source and destination) and store them.
4. Create a graph using the input edge list.
5. Print the adjacency list representation of the graph.
6. End the program.

## Program:
```

int main(void)
{
    int n, i, N;
    scanf("%d", &N);
    scanf("%d", &n);

    // input array containing edges of the graph
    // (x, y) pair in the array represents an edge from x to y
    struct Edge edges[n];

    for (i = 0; i < n; i++)
    {
        // get the source and destination vertex
        scanf("%d", &edges[i].src);
        scanf("%d", &edges[i].dest);
    }

    // construct a graph from the given edges
    struct Graph* graph = createGraph(edges, n);

    // Function to print adjacency list representation of a graph
    printGraph(graph);

    return 0;
}

```

## Output:

![image](https://github.com/user-attachments/assets/39f0befa-6f74-4a5b-aeb9-db001a08a8df)

## Result:
Thus, the C program to represent the given graph using the adjacency list is implemented successfully
