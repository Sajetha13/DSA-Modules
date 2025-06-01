# Travelling Salesman Problem
## AIM:
To write a C Program to implement Travelling Salesman Problem for finding shortest path.

## Algorithm
1. Declare global variables: a[10][10], visited[10] (all 0), n, and cost = 0.
2. In get(), read number of cities n, input cost matrix a[i][j], and initialize visited[].
3. In mincost(city), mark city visited, print it, find next city using least(city), update cost, and recurse.
4. In least(city), check unvisited cities, find one with minimum cost, return its index. 
5. In main, call get(), then mincost(0), and finally put() to print total minimum cost. 

## Program:
```
#include<stdio.h>
int a[10][10],visited[10],n,cost=0;

void get()
{
	int i,j;
		scanf("%d",&n);
	for(i=0;i < n;i++)
	{
			for( j=0;j < n;j++)
			scanf("%d",&a[i][j]);
		visited[i]=0;
	}
	}

void mincost(int city)
{
	int ncity;
	int least(int);
	visited[city]=1;	
	printf("%d -->",city+1);
	ncity=least(city);
	if(ncity==999)
	{
		ncity=0;
		printf("%d",ncity+1);
		cost+=a[city][ncity];
		return;
	}
	mincost(ncity);
}

int least(int c)
{
	int i,nc=999;
	int min=999,kmin;
	for(i=0;i < n;i++)
	{
		if((a[c][i]!=0)&&(visited[i]==0))
			if(a[c][i] < min)
			{
				min=a[i][0]+a[c][i];
				kmin=a[c][i];
				nc=i;
			}
	}
	if(min!=999)
		cost+=kmin;
	return nc;
}

void put()
{
	printf("\n\nMinimum cost:%d",cost);
	}

int main()
{
	get();
	mincost(0);
	put();
	return 0;
	}

```

## Output:

![image](https://github.com/user-attachments/assets/3c143d65-298c-41fb-9de1-67213ba4b210)

## Result:
Thus, the C program to implement Travelling Salesman Problem for finding shortest path is implemented successfully.
