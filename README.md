 ## Ex-6-IMPLEMENTATION-OF-THE-BACK-END-OF-THE-COMPILER-
## IMPLEMENTATION OF THE BACK END OF THE COMPILER

# Date :12-03-2026
# Aim :
To write a program to implement the back end of the compiler.

# ALGORITHM
Start the program.
Get the three variables from statements and stored in the text file k.txt.
Compile the program and give the path of the source file.
Execute the program.
Target code for the given statement is produced.
Stop the program.
# PROGRAM
# exp6 code
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main() {
    char line[100], var[10], op1[10], op2[10], res[10], op;
    char filename[50];
    FILE *fp;
    int reg = 0;

    printf("Enter the filename of the intermediate code: ");
    scanf("%s", filename);

    fp = fopen(filename, "r");
    if (fp == NULL) {
        printf("Error: Could not open file.\n");
        return 1;
    }

    printf("\nIntermediate Code:\n\n");

    while (fgets(line, sizeof(line), fp)) {
        printf("\t\t%s", line);
    }

    rewind(fp);

    printf("\n\n\tStatement\t\tTarget Code\n\n");

    while (fgets(line, sizeof(line), fp)) {
        // Remove newline if exists
        line[strcspn(line, "\n")] = 0;

        // Example format: t1 = a + b
        if (sscanf(line, "%s = %s %c %s", res, op1, &op, op2) == 4) {
            printf("\t%s\t\tMOV %s, R%d\n", line, op2, reg);
            printf("\t\t\t\t");

            if (op == '+')
                printf("ADD ");
            else if (op == '-')
                printf("SUB ");
            else if (op == '*')
                printf("MUL ");
            else if (op == '/')
                printf("DIV ");
            else
                printf("OP? ");

            printf("%s, R%d\n\n", op1, reg);
            reg++;
        }
    }

    fclose(fp);
    return 0;
}
```
# exp6ip.txt
```
t1 = a + b
t2 = t1 - c
```
## OUTPUT
![exp6](https://github.com/user-attachments/assets/362e0523-599b-4a7b-a350-2a7d5987e4f1)


## Result
The back end of the compiler is implemented successfully, and the output is verified.
