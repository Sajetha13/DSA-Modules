# Evaluation of Prefix Expression using Stack

## Aim:
To write a C program to evaluate a prefix arithmetic expression using stack operations and display the output within the evaluation function.

## Algorithm:
1. Read the prefix expression from the user.
2. Traverse the expression from right to left.
3. If the current character is an operand, push it onto the stack.
4. If the current character is an operator, pop two operands from the stack.
5. Perform the operation and push the result back onto the stack.
6. After completing the traversal, pop the final result from the stack and print it.

## Program:
```c
#include<stdio.h>
#include<string.h>
#include<ctype.h>

int s[50];
int top=0;

void push(int ch)
{
    top++;
    s[top]=ch;
}

int pop()
{
    int ch;
    ch=s[top];
    top=top-1;
    return(ch);
}

void evalprefix(char p[50])
{
    int n1, n2, n3;
    for(int i=strlen(p)-1; i>=0; i--){
        if(isdigit(p[i])){
            push(p[i]-'0');
        }
        else if (p[i] != ' ' && p[i] != '\n'){
            n1=pop();
            n2=pop();
            switch(p[i]){
                case '+':
                    n3=n1+n2;
                    break;
                case '-':
                    n3=n1-n2;
                    break;
                case '*':
                    n3=n1*n2;
                    break;
                case '/':
                    n3=n1/n2;
                    break;
            }
            push(n3);
        }
    }
    printf("%d", pop());
}

int  main()
{
    char e[50];
    fgets(e,sizeof(e),stdin);
    evalprefix(e);
    return 0;
}
```

## Output:
![Screenshot 2025-06-01 162054](https://github.com/user-attachments/assets/d5e61807-18c3-4725-8ad8-1d2e12acab90)


## Result:
The C program was successfully written and executed to evaluate a prefix expression using stack and displayed the correct result.
