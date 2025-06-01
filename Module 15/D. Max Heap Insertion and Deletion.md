# Max Heap Insertion and Deletion

## Aim
To write a C program to insert and delete elements in a Max Heap Tree and display the updated Max-Heap array.

---

## Algorithm

### 1. **Insert Operation**:
- Add the new element at the end of the array.
- Re-heapify from the last internal node up to the root to maintain the Max Heap property.

### 2. **Delete Operation**:
- Search for the element to delete.
- Swap it with the last element.
- Decrease heap size.
- Re-heapify from the last internal node up to the root to maintain Max Heap property.

### 3. **Heapify Function**:
- For a given node `i`, calculate the left and right child indices.
- Determine the largest among the current node and its children.
- Swap and recursively heapify if the largest is not the current node.

### 4. **Print Function**:
- Traverse the array and print each element.

---

## Program

```c
#include <stdio.h>

int size = 0;

void swap(int *a, int *b)
{
  int temp = *b;
  *b = *a;
  *a = temp;
}

void heapify(int array[], int size, int i)
{
  if (size == 1)
  {
    printf("Single element in the heap");
  }
  else
  {
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    if (l < size && array[l] > array[largest])
      largest = l;
    if (r < size && array[r] > array[largest])
      largest = r;
    if (largest != i)
    {
      swap(&array[i], &array[largest]);
      heapify(array, size, largest);
    }
  }
}

void insert(int array[], int newNum)
{
  if (size == 0)
  {
    array[0] = newNum;
    size += 1;
  }
  else
  {
    array[size] = newNum;
    size += 1;
    for (int i = size / 2 - 1; i >= 0; i--)
    {
      heapify(array, size, i);
    }
  }
}

void deleteRoot(int array[], int num)
{
  int i;
  for (i = 0; i < size; i++)
  {
    if (array[i] == num)
      break;
  }
  swap(&array[i], &array[size - 1]);
  size--;
  for (i = size / 2 - 1; i >= 0; i--)
  {
    heapify(array, size, i);
  }
}

void printArray(int array[], int size)
{
  for (int i = 0; i < size; ++i)
    printf("%d ", array[i]);
  printf("\n");
}

int main()
{
  int array[10], n, data, x;
  scanf("%d", &n);
  for (int i = 0; i < n; i++)
  {
    scanf("%d", &data);
    insert(array, data);
  }

  scanf("%d", &x);
  deleteRoot(array, x);

  printf("After deleting an element: ");
  printArray(array, size);
}
```
---
## Output
![image](https://github.com/user-attachments/assets/3b753848-c201-4ab0-a10e-8d00851e1554)


---
## Result
The program successfully inserts elements into a Max Heap, deletes a specified element, and maintains the Max-Heap structure after the deletion.
