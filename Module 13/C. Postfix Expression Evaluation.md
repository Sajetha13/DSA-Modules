# Postfix Expression Evaluation

## Aim

To write a C program to evaluate a postfix expression using a stack. The expression involves only addition (+) and division (/).

---

## Algorithm

1. **Start**
2. Initialize an empty stack.
3. Read the postfix expression from left to right.
4. If the character is an operand, push it onto the stack.
5. If the character is an operator:

   * Pop two elements from the stack.
   * Apply the operator.
   * Push the result back onto the stack.
6. Repeat steps 4-5 until the end of the expression.
7. The result of the expression will be at the top of the stack.
8. **End**

---

## Program

```c
#include<stdio.h>
#include<ctype.h>

int stack[20];
int top = -1;

void push(int x)
{
    stack[++top] = x;
}

int pop()
{
    return stack[top--];
}

void evalpostfix(char *e)
{
    int n1, n2, n3;
    while (*e != '\0'){
        if (isdigit(*e)){
            push(*e - '0');
        }
        else{
            n1 = pop();
            n2 = pop();
            switch (*e){
                case '+':
                    n3 = n2 + n1;
                    break;
                case '/':
                    n3 = n2 / n1;
                    break;
            }
            push(n3);
        }
        e++;
    }
    printf("Result of postfix expression: %d\n", pop());
}

int main()
{
    char expr[] = "45+21/+";
    evalpostfix(expr);
    return 0;
}
```

---

## Output

![image](https://github.com/user-attachments/assets/532f3c6f-c0cc-4386-a3a2-be4cefa38f9c)


---

## Result

Thus, the C program to evaluate the postfix expression using stack was successfully implemented and executed.
