# Max Heap Insertion

## Aim
To write a C program to insert elements into a Max Heap Tree and display the resulting Max-Heap array.

---

## Algorithm

1. **Initialize**:
   - Create an array to represent the heap.
   - Use a global `size` variable to track the number of elements in the heap.

2. **Insert Function**:
   - If heap is empty, place the element at the first position.
   - Else, insert the new element at the end of the array.
   - Call `heapify()` on all internal nodes from bottom to top to maintain the Max Heap property.

3. **Heapify Function**:
   - For a given node `i`, find the indices of the left and right children.
   - Compare the values at the current node and its children.
   - Swap the current node with the largest child if necessary.
   - Recursively heapify the affected subtree.

4. **Print Function**:
   - Traverse the array and print each element.

---

## Program

```c
#include <stdio.h>

int size = 0;

void swap(int *a, int *b) {
    int temp = *b;
    *b = *a;
    *a = temp;
}

void heapify(int array[], int size, int i) {
    if (size == 1) {
        printf("Single element in the heap");
    } else {
        int largest = i;
        int l = 2 * i + 1;
        int r = 2 * i + 2;

        if (l < size && array[l] > array[largest])
            largest = l;
        if (r < size && array[r] > array[largest])
            largest = r;

        if (largest != i) {
            swap(&array[i], &array[largest]);
            heapify(array, size, largest);
        }
    }
}

void insert(int array[], int newNum) {
    if (size == 0) {
        array[0] = newNum;
        size += 1;
    } else {
        array[size] = newNum;
        size++;
        for (int i = (size - 1) / 2; i >= 0; i--) {
            heapify(array, size, i);
        }
    }
}

void printArray(int array[], int size) {
    for (int i = 0; i < size; ++i)
        printf("%d ", array[i]);
    printf("\n");
}

int main() {
    int array[10], n, data;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &data);
        insert(array, data);
    }

    printf("Max-Heap array: ");
    printArray(array, size);
}
```
---
## Output

![image](https://github.com/user-attachments/assets/4ebcd8c1-4e58-4c21-a50b-ef9eacf3b155)

---
## Result
The program successfully inserts elements into a Max Heap and displays the Max-Heap structure after all insertions.
