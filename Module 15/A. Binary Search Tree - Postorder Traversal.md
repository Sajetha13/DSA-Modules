# Binary Search Tree - Postorder Traversal

## Aim
To construct a Binary Search Tree (BST) by inserting elements and then perform postorder traversal to print the nodes in postorder.

## Algorithm

1. **Insertion into BST**:
   - If the tree is empty, create a new node and return it.
   - If the value is less than or equal to the root, insert in the left subtree.
   - Otherwise, insert in the right subtree.

2. **Postorder Traversal**:
   - Recursively visit the left subtree.
   - Recursively visit the right subtree.
   - Print the data of the current node.

## Program

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *left;
    struct node *right;
};

struct node* insert(struct node* root, int data) {
    if (root == NULL) {
        struct node* node = (struct node*)malloc(sizeof(struct node));
        node->data = data;
        node->left = NULL;
        node->right = NULL;
        return node;
    } else {
        if (data <= root->data) {
            root->left = insert(root->left, data);
        } else {
            root->right = insert(root->right, data);
        }
        return root;
    }
}

void postOrder(struct node *root) {
    if (root != NULL) {
        postOrder(root->left);
        postOrder(root->right);
        printf("%d ", root->data);
    }
}

int main() {
    struct node* root = NULL;
    int t, data;

    scanf("%d", &t);
    while (t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }

    postOrder(root);
    return 0;
}
```
## Output

![image](https://github.com/user-attachments/assets/f41e27be-b4e2-4a54-82fc-f233ddb7c122)

## Result
The program successfully constructs a binary search tree from the given input and prints the elements using postorder traversal.
