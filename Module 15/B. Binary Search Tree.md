# Binary Search Tree (BST) - Deletion

## Aim
To write a program in C to delete an element from a Binary Search Tree (BST) and perform inorder traversal to display the resulting tree.

---

## Algorithm

### BST Insertion:
1. Start from the root node.
2. If the root is NULL, create a new node and return it.
3. If the value to insert is less than the current node’s value, insert into the left subtree.
4. If the value is greater, insert into the right subtree.
5. Return the updated tree root.

### BST Deletion:
1. Find the node to be deleted by traversing the tree:
   - If the value is less, move to the left.
   - If greater, move to the right.
2. Once found, handle three cases:
   - **No child**: Free the node.
   - **One child**: Replace node with its child.
   - **Two children**:
     - Find the inorder successor (smallest value in right subtree).
     - Replace node’s value with the successor’s.
     - Recursively delete the successor.

### Inorder Traversal:
1. Traverse the left subtree.
2. Print the current node’s value.
3. Traverse the right subtree.

---

## Program

```c
#include <stdio.h>
#include <stdlib.h>

struct btnode {
    int value;
    struct btnode *l, *r;
};

struct btnode* insert(struct btnode* root, int data);
struct btnode* deleteNode(struct btnode* root, int data);
struct btnode* minValueNode(struct btnode* node);
void inorder(struct btnode* root);

int main() {
    int n, data;
    struct btnode* root = NULL;

    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        scanf("%d", &data);
        root = insert(root, data);
    }

    scanf("%d", &data);
    root = deleteNode(root, data);

    inorder(root);

    return 0;
}

struct btnode* insert(struct btnode* root, int data) {
    if (root == NULL) {
        struct btnode* temp = (struct btnode*)malloc(sizeof(struct btnode));
        temp->value = data;
        temp->l = temp->r = NULL;
        return temp;
    }

    if (data < root->value)
        root->l = insert(root->l, data);
    else if (data > root->value)
        root->r = insert(root->r, data);

    return root;
}

void inorder(struct btnode* root) {
    if (root != NULL) {
        inorder(root->l);
        printf("%d -> ", root->value);
        inorder(root->r);
    }
}

struct btnode* minValueNode(struct btnode* node) {
    struct btnode* current = node;
    while (current && current->l != NULL)
        current = current->l;
    return current;
}

struct btnode* deleteNode(struct btnode* root, int data) {
    if (root == NULL)
        return root;

    if (data < root->value)
        root->l = deleteNode(root->l, data);
    else if (data > root->value)
        root->r = deleteNode(root->r, data);
    else {
        if (root->l == NULL) {
            struct btnode* temp = root->r;
            free(root);
            return temp;
        } else if (root->r == NULL) {
            struct btnode* temp = root->l;
            free(root);
            return temp;
        }

        struct btnode* temp = minValueNode(root->r);
        root->value = temp->value;
        root->r = deleteNode(root->r, temp->value);
    }
    return root;
}
```

## Output

![image](https://github.com/user-attachments/assets/eaa88745-d7d8-4a4d-9196-ac394d84d96f)

## Result
The program successfully implements insertion and deletion operations in a Binary Search Tree (BST) and performs an inorder traversal to display the tree after deletion.
