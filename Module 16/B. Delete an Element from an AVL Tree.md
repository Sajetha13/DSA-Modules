# Delete an Element from an AVL Tree

## Aim
To write a C program to delete an element from an AVL Tree and display the tree after deletion in preorder traversal with balance factors.

---

## Algorithm

1. **Insertion in AVL Tree:**
   - Insert the node like a binary search tree.
   - Update the height of the ancestor nodes.
   - Check the balance factor.
   - Perform necessary rotations (LL, RR, LR, RL) to maintain AVL property.

2. **Deletion in AVL Tree:**
   - Perform standard BST deletion.
   - If node has one or no child, remove it directly.
   - If node has two children, replace with inorder successor and delete successor.
   - Update the height of nodes and balance factors.
   - Perform rotations if balance factor is violated after deletion.

3. **Rotations:**
   - Right Rotation (LL case)
   - Left Rotation (RR case)
   - Left-Right Rotation (LR case)
   - Right-Left Rotation (RL case)

4. **Traversal:**
   - Preorder traversal to display nodes with their balance factors.

---

## Program

```c
#include<stdio.h>
#include<stdlib.h>

typedef struct node
{
    int data;
    struct node *left,*right;
    int ht;
}node;

node *insert(node *, int);
node *Delete(node *, int);
void preorder(node *);
int height(node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);

int main()
{
    node *root = NULL;
    int x, n, i;
    scanf("%d", &n);
    root = NULL;
    for(i = 0; i < n; i++)
    {
        scanf("%d", &x);
        root = insert(root, x);
    }
    scanf("%d", &x);
    root = Delete(root, x);
    preorder(root);
    return 0;
}

node *insert(node *T, int x)
{
    if(T == NULL)
    {
        T = (node*)malloc(sizeof(node));
        T->data = x;
        T->left = NULL;
        T->right = NULL;
        T->ht = 0;
    }
    else if(x > T->data)
    {
        T->right = insert(T->right, x);
        if(BF(T) == -2)
        {
            if(x > T->right->data)
                T = RR(T);
            else
                T = RL(T);
        }
    }
    else if(x < T->data)
    {
        T->left = insert(T->left, x);
        if(BF(T) == 2)
        {
            if(x < T->left->data)
                T = LL(T);
            else
                T = LR(T);
        }
    }
    T->ht = height(T);
    return T;
}

node *Delete(node *T, int x)
{
    if(T == NULL)
        return NULL;
    if(x > T->data)
        T->right = Delete(T->right, x);
    else if(x < T->data)
        T->left = Delete(T->left, x);
    else
    {
        if((T->left == NULL) || (T->right == NULL))
        {
            node* temp = (T->left) ? T->left : T->right;
            free(T);
            return temp;
        }
        else
        {
            node* p = T->right;
            while(p->left != NULL)
                p = p->left;
            T->data = p->data;
            T->right = Delete(T->right, p->data);
        }
    }
    T->ht = height(T);
    int bf = BF(T);
    if(bf == 2)
    {
        if(BF(T->left) >= 0)
            return LL(T);
        else
            return LR(T);
    }
    else if(bf == -2)
    {
        if(BF(T->right) <= 0)
            return RR(T);
        else
            return RL(T);
    }
    return T;
}

int height(node *T)
{
    int lh, rh;
    if(T == NULL)
        return 0;
    lh = (T->left) ? 1 + T->left->ht : 0;
    rh = (T->right) ? 1 + T->right->ht : 0;
    return (lh > rh) ? lh : rh;
}

node *rotateright(node *x)
{
    node *y = x->left;
    x->left = y->right;
    y->right = x;
    x->ht = height(x);
    y->ht = height(y);
    return y;
}

node *rotateleft(node *x)
{
    node *y = x->right;
    x->right = y->left;
    y->left = x;
    x->ht = height(x);
    y->ht = height(y);
    return y;
}

node *RR(node *T)
{
    return rotateleft(T);
}

node *LL(node *T)
{
    return rotateright(T);
}

node *LR(node *T)
{
    T->left = rotateleft(T->left);
    return rotateright(T);
}

node *RL(node *T)
{
    T->right = rotateright(T->right);
    return rotateleft(T);
}

int BF(node *T)
{
    int lh, rh;
    if(T == NULL)
        return 0;
    lh = (T->left) ? 1 + T->left->ht : 0;
    rh = (T->right) ? 1 + T->right->ht : 0;
    return lh - rh;
}

void preorder(node *T)
{
    if(T != NULL)
    {
        printf("%d(Bf=%d)", T->data, BF(T));
        preorder(T->left);
        preorder(T->right);
    }
}
```
---
## Output

![image](https://github.com/user-attachments/assets/0a8a9bfc-5d5d-4397-92fb-b5ea35c8bda0)

## Result
The program successfully deletes a specified element from the AVL Tree while maintaining its balanced property, and prints the preorder traversal with balance factors.
