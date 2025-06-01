# B. Convert the Infix Expression to Postfix Expression and Display the Priority of the Operators

## Aim:

To convert the given infix expression into a postfix expression using stack operations and display the priority of operators.

## Algorithm:

1. **Start**
2. Initialize an empty stack for operators.
3. Scan the infix expression from left to right.
4. If the scanned character is an operand, add it to the postfix expression.
5. If the scanned character is an operator:

   * While the stack is not empty and the precedence of the current operator is less than or equal to the precedence of the operator at the top of the stack, pop operators from the stack and add them to the postfix expression.
   * Push the current operator onto the stack.
6. If the scanned character is '(', push it to the stack.
7. If the scanned character is ')', pop and output from the stack until an '(' is encountered.
8. After the entire infix expression has been scanned, pop and output all remaining operators in the stack.
9. **End**

## Program:

```c
#include<stdio.h>
#include<ctype.h>
#include <stdlib.h>

char stack[100];
int top = -1;

void push(char x)
{
    if (top == 99){
        printf("Stack overflow\n");
        exit(1);
    }
    stack[++top]=x;
}

char pop()
{
    if (top == -1){
        printf("Stack underflow\n");
        return '\0';
    }
    return stack[top--];
}

int priority(char x)
{
    switch(x){
        case '^':
            return 3;
        case '*':
        case '/':
        case '%':
            return 2;
        case '+':
        case '-':
            return 1;
        default:
            break;
    }
    return 0;
}

char IntoPost(char *exp)
{
    char *e, next;
    e = exp;
    while (*e != '\0')
    {
        if (isalnum(*e)){
            printf("%c ", *e);
        }
        else
        {
            switch(*e)
            {
                case '(':
                    push(*e);
                    break;
                case ')':
                    while((next = pop()) != '('){
                        printf("%c ", next);
                    }
                    break;
                case '%':
                case '/':
                case '^':
                case '*':
                case '-':
                case '+':
                    while(priority(stack[top]) >= priority(*e)){
                        printf("%c ", pop());
                    }
                    push(*e);
                    break;
            }
        }
        e++;
    }
    while(top != -1)
    {
        printf("%c ", pop());
    }
    return 0;
}

int main()
{
    char exp[100] = "(P%Q)/A*B^C+(R-S/U)+W^V";
    IntoPost(exp);
    return 0;
}
```

## Output:

*Attach output image here*

## Result:

The infix expression was successfully converted into a postfix expression and the operator priorities were correctly applied using stack operations.
