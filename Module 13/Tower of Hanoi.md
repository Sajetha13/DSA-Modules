# Tower of Hanoi

## Aim:

To write a C program to solve the Tower of Hanoi problem using recursion.

## Algorithm:

1. Define a recursive function `TOH(n, source, destination, auxiliary)`.
2. If `n > 0`, do the following:

   * Move `n-1` disks from source to auxiliary using destination as temporary.
   * Move the nth disk from source to destination.
   * Move `n-1` disks from auxiliary to destination using source as temporary.
3. Base case automatically ends when `n` reaches 0.

## Program:

```c
#include<stdio.h>

void TOH(int n, char sour, char dest, char aux){
    if (n > 0){
        TOH(n - 1, sour, aux, dest);
        printf("%c to %c\n", sour, dest);
        TOH(n - 1, aux, dest, sour);
    }
}

int main(){
    int n;
    scanf("%d", &n);
    TOH(n, 'A', 'B', 'C');
    return 0;
}
```

## Output:

(Add output image here)

## Result:

The Tower of Hanoi problem was successfully solved using a recursive C program.
