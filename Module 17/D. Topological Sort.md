
# Topological Sort
## AIM:
To compose the code to determine whether the topological ordering for the following graph is possible or not.

![image](https://github.com/user-attachments/assets/c74a7111-9b59-475c-aad4-9baf23d50ec0)


## Algorithm
1. Start the program.
2. Initialize required variables.
3. Run loop to sort elements topologically.
4. Keep track of the count of vertices added. If count is less than the total number of vertices in the graph then no topological ordering is possible, the graph contains cycles.
5. End the program.

## Program:
```
//#include<stdio.h>
//#include<stdlib.h>

//#define MAX 5

//int n;    /*Number of vertices in the graph*/
//int adj[MAX][MAX]; /*Adjacency Matrix*/
//void create_graph();

//int queue[MAX], front = -1,rear = -1;
//void insert_queue(int v);
//int delete_queue();
//int isEmpty_queue();

//int indegree(int v);

int main()
{
        int i,v,count,topo_order[MAX],indeg[MAX];

        create_graph();

        /*Find the indegree of each vertex*/
        for(i=0;i<n;i++)
        {
                indeg[i] = indegree(i);
                if( indeg[i] == 0 )
                        insert_queue(i);
        }

        count = 0;

        while(  !isEmpty_queue( ) && count < n )
        {
                v = delete_queue();
        topo_order[++count] = v; /*Add vertex v to topo_order array*/
                /*Delete all edges going from vertex v */
                for(i=0; i<n; i++)
                {
                        if(adj[v][i] == 1)
                        {
                                adj[v][i] = 0;
                                indeg[i] = indeg[i]-1;
                                if(indeg[i] == 0)
                                        insert_queue(i);
                        }
                }
        }
        if(count<n)
        {
            printf("No topological ordering possible, graph contains cycle");
            exit(1);
        }
        printf("Vertices in topological order is :\n");
        for(i=1;i<=n;i++)
        {
            printf("%d ",topo_order[i]);
        }
}/*End of main()*/

```

## Output:

![image](https://github.com/user-attachments/assets/b651e971-7046-4f75-9edf-8c52104b5c67)

## Result:
Thus, the C program for determining whether the topological ordering for the following graph is possible or not, is implemented successfully.
