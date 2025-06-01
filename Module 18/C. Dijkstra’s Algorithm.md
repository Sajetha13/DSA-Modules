# Dijkstra’s Algorithm
## AIM:
To write a C Program to implement Dijkstra's Algorithm to find the shortest path

## Algorithm
1. Define INFINITY = 9999, MAX = 10; declare G[MAX][MAX], distance[], visited[], pred[].
2. Input number of nodes n and the adjacency matrix; replace 0s with INFINITY; read starting node u.
3. Initialize distance[i] = G[u][i], pred[i] = u, visited[i] = 0; set distance[u] = 0 and mark u visited. 
4. Repeat for n-1 nodes: find nearest unvisited node, mark it visited, and update distances of neighbors.
5. For each node except start, print shortest distance and path using pred[].  

## Program:
```
#include<stdio.h>
#define INFINITY 9999
#define MAX 10
 
void dijkstra(int G[MAX][MAX],int n,int startnode);
 
int main()
{
int G[MAX][MAX],i,j,n,u;
scanf("%d",&n);
for(i=0;i<n;i++)
for(j=0;j<n;j++)
scanf("%d",&G[i][j]);
scanf("%d",&u);
dijkstra(G,n,u);
return 0;
}
 
void dijkstra(int G[MAX][MAX],int n,int startnode)
{
 
int cost[MAX][MAX],distance[MAX],pred[MAX];
int visited[MAX],count,mindistance,nextnode,i,j;
//pred[] stores the predecessor of each node
//count gives the number of nodes seen so far
//create the cost matrix
for(i=0;i<n;i++)
for(j=0;j<n;j++)
if(G[i][j]==0)
cost[i][j]=INFINITY;
else
cost[i][j]=G[i][j];
//initialize pred[],distance[] and visited[]
for(i=0;i<n;i++)
{
distance[i]=cost[startnode][i];
pred[i]=startnode;
visited[i]=0;
}
distance[startnode]=0;
visited[startnode]=1;
count=1;
while(count<n-1)
{
mindistance=INFINITY;
//nextnode gives the node at minimum distance
for(i=0;i<n;i++)
if(distance[i]<mindistance&&!visited[i])
{
mindistance=distance[i];
nextnode=i;
}
//check if a better path exists through nextnode
visited[nextnode]=1;
for(i=0;i<n;i++)
if(!visited[i])
if(mindistance+cost[nextnode][i]<distance[i])
{
distance[i]=mindistance+cost[nextnode][i];
pred[i]=nextnode;
}
count++;
}
 
//print the path and distance of each node
for(i=0;i<n;i++)
if(i!=startnode)
{
printf("Distance of node%d=%d\n",i,distance[i]);
printf("Path=%d",i);
j=i;
do
{
j=pred[j];
printf("<-%d",j);
}while(j!=startnode);
}
}

```

## Output:

![image](https://github.com/user-attachments/assets/2e7e2afe-db80-42f0-97c7-b857b2b1b0f4)

## Result:
Thus, the Program to implement Dijkstra's Algorithm to find the shortest path is implemented successfully.
