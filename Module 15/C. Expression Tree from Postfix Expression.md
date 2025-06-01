# Expression Tree from Postfix Expression

## Aim
To write a C program to construct an Expression Tree for the given Postfix Expression and display the In-order, Pre-order, and Post-order traversals.

---

## Algorithm

### Expression Tree Construction:
1. Read the postfix expression from the user.
2. Initialize an empty stack to hold tree nodes.
3. For each character in the postfix expression:
   - If it is an operand (alphabet or digit), create a node and push it onto the stack.
   - If it is an operator:
     - Pop two nodes from the stack.
     - Make the operator node the parent and the popped nodes its children.
     - Push the resulting subtree back to the stack.
4. After the expression is parsed, the top of the stack is the root of the expression tree.

### Tree Traversals:
- **In-order (Left, Root, Right)**:
  Recursively traverse the left subtree, visit the root, then the right subtree.
- **Pre-order (Root, Left, Right)**:
  Visit the root first, then recursively traverse the left and right subtrees.
- **Post-order (Left, Right, Root)**:
  Recursively traverse left and right subtrees, then visit the root.

---

## Program

```c
#include <stdio.h>
#include <stdlib.h>

struct n {
    char d;
    struct n *l;
    struct n *r;
};

char pf[50];
int top = -1;
struct n *a[50];

int r(char inputch) {
    if (inputch == '+' || inputch == '-' || inputch == '*' || inputch == '/')
        return -1;
    else if ((inputch >= 'A' && inputch <= 'Z') || (inputch >= 'a' && inputch <= 'z') || (inputch >= '0' && inputch <= '9'))
        return 1;
    else
        return -100;
}

void push(struct n *tree) {
    top++;
    a[top] = tree;
}

struct n *pop() {
    top--;
    return a[top + 1];
}

void construct_expression_tree(char *suffix) {
    char s;
    struct n *newl, *p1, *p2;
    int flag;
    s = suffix[0];
    for (int i = 1; s != 0; i++) {
        flag = r(s);
        if (flag == 1) {
            newl = (struct n *)malloc(sizeof(struct n));
            newl->d = s;
            newl->l = NULL;
            newl->r = NULL;
            push(newl);
        } else {
            p1 = pop();
            p2 = pop();
            newl = (struct n *)malloc(sizeof(struct n));
            newl->d = s;
            newl->l = p2;
            newl->r = p1;
            push(newl);
        }
        s = suffix[i];
    }
}

void preOrder(struct n *tree) {
    if (tree != NULL) {
        printf("%c", tree->d);
        preOrder(tree->l);
        preOrder(tree->r);
    }
}

void inOrder(struct n *tree) {
    if (tree != NULL) {
        inOrder(tree->l);
        printf("%c", tree->d);
        inOrder(tree->r);
    }
}

void postOrder(struct n *tree) {
    if (tree != NULL) {
        postOrder(tree->l);
        postOrder(tree->r);
        printf("%c", tree->d);
    }
}

int main() {
    scanf("%s", pf);
    construct_expression_tree(pf);

    inOrder(a[0]);
    printf("\n");

    preOrder(a[0]);
    printf("\n");

    postOrder(a[0]);
    printf("\n");

    return 0;
}
```
---

## Output
![image](https://github.com/user-attachments/assets/f85668f0-5d7a-4d19-80a3-37f025d31a88)


---

## Result
The program successfully constructs an Expression Tree from the given Postfix Expression and performs In-order, Pre-order, and Post-order traversals of the tree.
