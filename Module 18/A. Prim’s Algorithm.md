# Prim's Algorithm - Minimum Spanning Tree

## Aim

To implement Prim's algorithm in C to find the Minimum Spanning Tree (MST) of a given connected, undirected, and weighted graph.

## Algorithm

1. Input the number of vertices and the adjacency matrix of the graph.
2. Convert the adjacency matrix to a cost matrix:

   * If `G[i][j] == 0`, set `cost[i][j]` to infinity.
3. Initialize arrays:

   * `visited[]` to mark visited vertices.
   * `distance[]` to hold the minimum cost edge to a vertex.
   * `from[]` to store the parent node in MST.
4. Start from vertex 0:

   * Mark it visited.
   * Set initial distances.
5. Repeat for `n-1` edges:

   * Find the unvisited vertex with the smallest distance.
   * Add its edge to the spanning tree.
   * Mark it as visited.
   * Update `distance[]` and `from[]` if a shorter edge is found.
6. Output the spanning tree and its total cost.

## Program

```c
#include <stdio.h>
#include <stdlib.h>

#define infinity 9999
#define MAX 20

int G[MAX][MAX], spanning[MAX][MAX], n;

int prims();

int main() {
    int i, j, total_cost;

    printf("Enter the number of vertices: ");
    scanf("%d", &n);

    printf("Enter the adjacency matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < n; j++)
            scanf("%d", &G[i][j]);

    total_cost = prims();

    printf("\nSpanning tree matrix:\n");
    for(i = 0; i < n; i++) {
        for(j = 0; j < n; j++)
            printf("%d ", spanning[i][j]);
        printf("\n");
    }

    printf("\nTotal cost of the spanning tree = %d\n", total_cost);

    return 0;
}

int prims() {
    int cost[MAX][MAX];
    int u, v, min_distance, distance[MAX], from[MAX];
    int visited[MAX], no_of_edges, i, min_cost, j;

    // Convert G to cost and initialize spanning to 0
    for(i = 0; i < n; i++)
        for(j = 0; j < n; j++) {
            if(G[i][j] == 0)
                cost[i][j] = infinity;
            else
                cost[i][j] = G[i][j];
            spanning[i][j] = 0;
        }

    distance[0] = 0;
    visited[0] = 1;

    for(i = 1; i < n; i++) {
        distance[i] = cost[0][i];
        from[i] = 0;
        visited[i] = 0;
    }

    min_cost = 0;
    no_of_edges = n - 1;

    while(no_of_edges > 0) {
        min_distance = infinity;

        for(i = 1; i < n; i++) {
            if(visited[i] == 0 && distance[i] < min_distance) {
                v = i;
                min_distance = distance[i];
            }
        }

        u = from[v];
        spanning[u][v] = distance[v];
        spanning[v][u] = distance[v];

        visited[v] = 1;
        no_of_edges--;
        min_cost += cost[u][v];

        for(i = 1; i < n; i++) {
            if(!visited[i] && cost[i][v] < distance[i]) {
                distance[i] = cost[i][v];
                from[i] = v;
            }
        }
    }

    return min_cost;
}
```

## Output:

![image](https://github.com/user-attachments/assets/ec66f784-57b1-4ee8-aee8-8f4715062c8b)

## Result:
Thus, the C program to implement Prim's Algorithm for finding Total Cost of tree is implemented successfully.
