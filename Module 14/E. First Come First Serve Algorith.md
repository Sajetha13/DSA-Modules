# CPU Scheduling: First Come First Serve (FCFS) Algorithm

## Aim
To implement the First Come First Serve (FCFS) CPU scheduling algorithm to calculate the waiting time, turnaround time, and average times for a set of processes.

## Algorithm
1. Initialize the waiting time for the first process as 0.
2. For each subsequent process, calculate its waiting time as the sum of the burst time of all previous processes.
3. Calculate turnaround time for each process as the sum of its burst time and waiting time.
4. Compute the average waiting time and average turnaround time.
5. Display the burst time, waiting time, and turnaround time for each process along with the average values.

## Program
```c
#include <stdio.h>

// Function to find the waiting time for all processes
int waitingtime(int proc[], int n, int burst_time[], int wait_time[]) {
   wait_time[0] = 0; // waiting time for first process is 0
   for (int i = 1; i < n ; i++ )
      wait_time[i] = burst_time[i-1] + wait_time[i-1];
   return 0;
}

// Function to calculate turn around time
int turnaroundtime(int proc[], int n, int burst_time[], int wait_time[], int tat[]) {
   for (int i = 0; i < n ; i++)
      tat[i] = burst_time[i] + wait_time[i];
   return 0;
}

// Function to calculate average time
int avgtime(int proc[], int n, int burst_time[]) {
   int wait_time[n], tat[n];
   int total_wt = 0, total_tat = 0;

   waitingtime(proc, n, burst_time, wait_time);
   turnaroundtime(proc, n, burst_time, wait_time, tat);

   printf("Processes  Burst   Waiting  Turnaround\n");
   for (int i = 0; i < n; i++) {
      total_wt += wait_time[i];
      total_tat += tat[i];
      printf(" %d\t\t %d\t\t %d\t\t %d\n", i+1, burst_time[i], wait_time[i], tat[i]);
   }

   printf("Average waiting time = %f\n", (float)total_wt / n);
   printf("Average turnaround time = %f\n", (float)total_tat / n);
   return 0;
}

int main() {
    int n;
    int proc[10], burst_time[10];

    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &proc[i]);
    }
    for (int i = 0; i < n; i++) {
        scanf("%d", &burst_time[i]);
    }

    avgtime(proc, n, burst_time);
    return 0;
}
```
## Output
![image](https://github.com/user-attachments/assets/223f9556-3e4c-4ba1-93be-adfdc9da32a4)

## Result
The program successfully calculates the waiting time, turnaround time, average waiting time, and average turnaround time for all processes using the FCFS scheduling algorithm.
