# Deque Implementation — Add Front Operation

## Aim
To implement the `addFront` operation in a deque (double-ended queue) using an array, allowing insertion of an element at the front end.

## Algorithm
1. Check if the deque is full by verifying if `front == 0` and `rear == MAX - 1`.
2. If full, print an overflow message and exit the function.
3. If deque is empty (`front == -1`), initialize `front` and `rear` to 0 and insert the item.
4. If rear is not at the last position (`rear != MAX - 1`):
   - Count the number of elements in the deque.
   - Shift elements one position towards the rear to create space at the front.
   - Insert the new item at the front.
   - Update `front` and `rear` indices.
5. If rear is at the last position:
   - Decrement `front`.
   - Insert the new item at the new `front` index.

## Program

```c
#include <stdio.h>
#define MAX 10

int count(int *arr); // Assume count function is defined elsewhere

void addFront(int *arr, int item, int *pfront, int *prear) {
    int i, k, c;

    if (*pfront == 0 && *prear == MAX - 1) {
        printf("deQueue is full.\n");
        return;
    }

    if (*pfront == -1) {
        *pfront = *prear = 0;
        arr[*pfront] = item;
        return;
    }

    if (*prear != MAX - 1) {
        c = count(arr);
        k = *prear + 1;
        for (i = 1; i <= c; i++) {
            arr[k] = arr[k - 1];
            k--;
        }
        arr[k] = item;
        *pfront = k;
        (*prear)++;
    } else {
        (*pfront)--;
        arr[*pfront] = item;
    }
}
```
## Output
![image](https://github.com/user-attachments/assets/09d4dadc-d43d-4df7-b6b7-08224a0694fb)

## Result
The addFront function correctly inserts an element at the front of the deque, handling overflow and shifting elements as needed.
