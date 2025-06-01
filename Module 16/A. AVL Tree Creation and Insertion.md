# AVL Tree Creation and Insertion

## Aim
To write a C program to create an AVL Tree using input elements and display the pre-order traversal along with the balance factor for each node.

---

## Algorithm

### Step 1: Start  
### Step 2: Accept number of nodes and the node values  
### Step 3: For each value, insert it into the AVL Tree  
- If the node is not present, create a new node.
- Recursively insert into the left or right subtree.
- After insertion, update the height.
- Balance the tree if the Balance Factor (BF) is ±2 using appropriate rotations:
  - **LL Rotation**: Left Left Case
  - **RR Rotation**: Right Right Case
  - **LR Rotation**: Left Right Case
  - **RL Rotation**: Right Left Case  

### Step 4: Print the AVL Tree in pre-order traversal with Balance Factors  
### Step 5: End  

---

## Program

```c
#include<stdio.h>
#include<stdlib.h>

typedef struct node {
    int data;
    struct node *left, *right;
    int ht;
} node;

node *insert(node *, int);
void preorder(node *);
int height(node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);

int main() {
    node *root = NULL;
    int x, n, i;
    scanf("%d", &n);
    for (i = 0; i < n; i++) {
        scanf("%d", &x);
        root = insert(root, x);
    }
    preorder(root);
    return 0;
}

node *insert(node *T, int x) {
    if (T == NULL) {
        T = (struct node *)malloc(sizeof(struct node));
        T->data = x;
        T->left = T->right = NULL;
    }
    else if (x > T->data) {
        T->right = insert(T->right, x);
        if (BF(T) == -2) {
            if (x > T->right->data)
                T = RR(T);
            else
                T = RL(T);
        }
    }
    else if (x < T->data) {
        T->left = insert(T->left, x);
        if (BF(T) == 2) {
            if (x < T->left->data)
                T = LL(T);
            else
                T = LR(T);
        }
    }
    T->ht = height(T);
    return T;
}

int height(node *T) {
    int lh, rh;
    if (T == NULL)
        return 0;
    lh = (T->left == NULL) ? 0 : 1 + T->left->ht;
    rh = (T->right == NULL) ? 0 : 1 + T->right->ht;
    return (lh > rh) ? lh : rh;
}

node *rotateright(node *x) {
    node *y = x->left;
    x->left = y->right;
    y->right = x;
    x->ht = height(x);
    y->ht = height(y);
    return y;
}

node *rotateleft(node *x) {
    node *y = x->right;
    x->right = y->left;
    y->left = x;
    x->ht = height(x);
    y->ht = height(y);
    return y;
}

node *RR(node *T) {
    return rotateleft(T);
}

node *LL(node *T) {
    return rotateright(T);
}

node *LR(node *T) {
    T->left = rotateleft(T->left);
    return rotateright(T);
}

node *RL(node *T) {
    T->right = rotateright(T->right);
    return rotateleft(T);
}

int BF(node *T) {
    int lh = (T == NULL || T->left == NULL) ? 0 : 1 + T->left->ht;
    int rh = (T == NULL || T->right == NULL) ? 0 : 1 + T->right->ht;
    return lh - rh;
}

void preorder(node *T) {
    if (T != NULL) {
        printf("%d(Bf=%d)", T->data, BF(T));
        preorder(T->left);
        preorder(T->right);
    }
}
```
---
## Output
![image](https://github.com/user-attachments/assets/9c2b314d-38be-4d27-9cd1-72a17974811f)

## Result
The program successfully creates an AVL Tree with the given inputs, applies rotations to maintain balance, and displays the pre-order traversal with each node's balance factor.
