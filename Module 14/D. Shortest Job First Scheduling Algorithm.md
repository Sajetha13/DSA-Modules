# Shortest Job First (SJF) Scheduling Algorithm

## Aim
To implement the Shortest Job First (SJF) scheduling algorithm by sorting the burst times of processes and calculating their waiting time and turnaround time.

## Algorithm
1. Read the number of processes and their burst times.
2. Initialize process numbers.
3. Sort the processes based on their burst times in ascending order using selection sort.
4. Set the waiting time of the first process to zero.
5. Calculate the waiting time for each process by summing the burst times of all previous processes.
6. Calculate turnaround time for each process as the sum of its burst time and waiting time.
7. Calculate the average waiting time and average turnaround time.
8. Display the process details, waiting time, turnaround time, and averages.

## Program

```c
#include<stdio.h>

int main()
{
    int bt[20], p[20], wt[20], tat[20], i, j, n, total=0, pos, temp;
    float avg_wt, avg_tat;

    scanf("%d", &n);

    for(i=0; i<n; i++)
    {
        scanf("%d", &bt[i]);
        p[i] = i + 1; // process number
    }

    // Sorting burst times in ascending order (Selection Sort)
    for(i=0; i<n-1; i++)
    {
        pos = i;
        for(j=i+1; j<n; j++)
        {
            if(bt[j] < bt[pos])
                pos = j;
        }
        temp = bt[i];
        bt[i] = bt[pos];
        bt[pos] = temp;

        temp = p[i];
        p[i] = p[pos];
        p[pos] = temp;
    }

    wt[0] = 0; // waiting time for first process

    // Calculate waiting times
    for(i=1; i<n; i++)
    {
        wt[i] = 0;
        for(j=0; j<i; j++)
            wt[i] += bt[j];

        total += wt[i];
    }

    avg_wt = (float)total / n;
    total = 0;

    printf("Process    Burst Time    Waiting Time  Turnaround Time\n");
    for(i=0; i<n; i++)
    {
        tat[i] = bt[i] + wt[i]; // turnaround time
        total += tat[i];
        printf("p%d          %d               %d             %d\n", p[i], bt[i], wt[i], tat[i]);
    }

    avg_tat = (float)total / n;

    printf("Average Waiting Time = %f\n", avg_wt);
    printf("Average Turnaround Time = %f\n", avg_tat);

    return 0;
}
```
## Output
![image](https://github.com/user-attachments/assets/e6636e8c-d1ca-4974-9c5c-418bb6bdd36e)
## Result
The program successfully implements the Shortest Job First scheduling algorithm by sorting processes according to their burst times, then calculating and displaying their waiting and turnaround times along with the averages.

