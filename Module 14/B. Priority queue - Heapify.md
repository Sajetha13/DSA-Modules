# Heapify in a Max-Heap after Deletion

## Aim:

To develop a C program to heapify the priority queue elements after deletion according to the max-heap property.

## Algorithm:

1. If the size of the heap is 1, print "Single element in the heap".
2. Otherwise, determine the largest element among the root (`i`), left child (`2*i + 1`), and right child (`2*i + 2`).
3. Store the index of the largest element in the variable `largest`.
4. If `largest` is not the root index `i`, swap the element at index `i` with the element at index `largest`.
5. Recursively call the heapify procedure on the affected subtree starting at `largest`.

## Program:

```c
#include <stdio.h>

void swap(int *a, int *b){
    int temp = *a;
    *a = *b;
    *b = temp;
}

void heapify(int array[], int size, int i) {
    if(size == 1) {
        printf("Single element in the heap");
    }
    else {
        int largest = i;
        int l = 2*i + 1;
        int r = 2*i + 2;
        
        if(l < size && array[l] > array[largest])
            largest = l;
            
        if(r < size && array[r] > array[largest])
            largest = r;
        
        if(largest != i) {
            swap(&array[i], &array[largest]);
            heapify(array, size, largest);
        }
    }
}
```
## Output:
![image](https://github.com/user-attachments/assets/81b61d69-9edb-4d34-a634-876fb0140e16)

### Result:
The heapify function successfully maintains the max-heap property after deletion by ensuring the root node is larger than its children.

