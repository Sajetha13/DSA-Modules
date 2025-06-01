### AIM

Write a C program to display the priority of the operators in the given infix expression using switch case statements.

The expression is: `K%L-M*N+(O^P)`

The function `priority(char x)` receives operators in the expression from the `main()` and returns the precedence value from lowest to highest.

| Operator | Precedence  |     
| -------- | ----------- | 
| &,       | 1 (Lowest)  |
| +, -     | 2           |            
| \*, /, % | 3           |            
| ^        | 4 (Highest) |          

---

### ALGORITHM

1. Define a function `priority(char x)` that returns a numeric priority.
2. In `main()`, define the infix expression as a string.
3. Traverse the string:

   * If the character is an operator, pass it to `priority()`.
   * Use `switch-case` to print its human-readable priority.
4. End the program.

---

### PROGRAM

```c
#include <stdio.h>
#include <string.h>

int priority(char x) {
    if (x == '&' || x == '|') return 1;
    if (x == '+' || x == '-') return 2;
    if (x == '*' || x == '/' || x == '%') return 3;
    if (x == '^') return 4;
    return 0;
}

int main() {
    char expr[] = "K%L-M*N+(O^P)";

    for (int i = 0; i < strlen(expr); i++) {
        if (strchr("+-*/%^&|", expr[i])) {
            printf("%c  ----> ", expr[i]);
            switch (priority(expr[i])) {
                case 1: printf("Lowest Priority\n"); break;
                case 2: printf("Second Lowest Priority\n"); break;
                case 3: printf("Second Highest Priority\n"); break;
                case 4: printf("Highest Priority\n"); break;
            }
        }
    }
    return 0;
}
```

---

### OUTPUT

(Add screenshot image here)

---

### RESULT

The program successfully displays the priority of each operator in the infix expression `K%L-M*N+(O^P)` using a switch-case approach.
