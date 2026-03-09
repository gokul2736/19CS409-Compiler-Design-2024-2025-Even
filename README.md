<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/bed54706-f4ea-4b5c-b6f3-58ac4f4f63c8" />## Compiler Design- All Exps

### Ex. No : 1	IMPLEMENTATION OF SYMBOL TABLE  
### Ex. No : 2  GENERATION OF LEXICAL TOKENS LEX/FLEX TOOL
### Ex. No : 3	RECOGNITION OF A VALID ARITHMETIC EXPRESSION THAT USES  
### Ex. No : 4  RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
### Ex. No : 5	RECOGNITION OF THE GRAMMAR (a<sup>n</sup>b where n>=10) USING YACC
### Ex. No : 6	IMPLEMENTATION OF THE BACK END OF THE COMPILER


---

# Ex. No : 1	
# IMPLEMENTATION OF SYMBOL TABLE 
## Register Number : 212224240086 
## Date : 10-03-2026

## AIM   
To write a C program to implement a symbol table.

## ALGORITHM
1.	Start the program.
2.	Get the input from the user with the terminating symbol ‘$’.
3.	Allocate memory for the variable by dynamic memory allocation function.
4.	If the next character of the symbol is an operator then only the memory is allocated.
5.	While reading, the input symbol is inserted into symbol table along with its memory address.
6.	The steps are repeated till ‘$’ is reached.
7.	To reach a variable, enter the variable to be searched and symbol table has been checked for corresponding variable, the variable along with its address is displayed as result.
8.	Stop the program. 

## PROGRAM
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

#define MAX_EXPRESSION_SIZE 100

int main()
{
    int i = 0, j = 0, x = 0, n, flag = 0;
    void *add[5];
    char b[MAX_EXPRESSION_SIZE], d[15], c, srch;

    printf("Enter the Expression terminated by $: ");

    while ((c = getchar()) != '$' && i < MAX_EXPRESSION_SIZE - 1)
    {
        b[i++] = c;
    }

    b[i] = '\0';
    n = i - 1;

    printf("Given Expression: %s\n", b);

    printf("\nSymbol Table\n");
    printf("Symbol\tAddress\tType\n");

    for (j = 0; j <= n; j++)
    {
        c = b[j];

        if (isalpha(c))
        {
            if (j == n || b[j + 1] == '+' || b[j + 1] == '-' || b[j + 1] == '*' || b[j + 1] == '=')
            {
                void *p = malloc(sizeof(char));

                if (p == NULL)
                {
                    printf("Memory allocation failed\n");
                    return 1;
                }

                add[x] = p;
                d[x] = c;

                printf("%c\t%p\tidentifier\n", c, p);
                x++;
            }
        }
    }

    printf("\nThe symbol to be searched: ");
    getchar();
    srch = getchar();

    for (i = 0; i < x; i++)
    {
        if (srch == d[i])
        {
            printf("Symbol Found\n");
            printf("%c @ address %p\n", srch, add[i]);
            flag = 1;
            break;
        }
    }

    if (flag == 0)
        printf("Symbol Not Found\n");

    for (i = 0; i < x; i++)
    {
        free(add[i]);
    }

    return 0;
}
```

## OUTPUT 
<img width="614" height="530" alt="image" src="https://github.com/user-attachments/assets/e3ae8ce4-2f92-47d4-81f2-6d0833406448" />

## RESULT
The program to implement a symbol table is executed and the output is verified.


---


# Ex. No : 2	
# GENERATION OF LEXICAL TOKENS LEX/FLEX TOOL
## Register Number : 212224240086
## Date : 

## AIM   
To write a lex program to implement lexical analyzer to recognize a few patterns.

## ALGORITHM
1.	Start the program.
2.	Lex program consists of three parts.
    a.	Declaration %%
    b.	Translation rules %%
    c.	Auxilary procedure.
3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form
    a.	P1 {action}
    b.	P2 {action}
    c.	…
    d.	…
    e.	Pn {action}
5.	Write a program in the vi editor and save it with .l extension.
6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.

## PROGRAM


## OUTPUT 

## RESULT
The lexical analyzer is implemented using lex and the output is verified.


---


# Ex. No : 3	
# RECOGNITION OF A VALID ARITHMETIC EXPRESSION THAT USES
## Register Number : 212224240086
## Date : 

## AIM   
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.

## PROGRAM


## OUTPUT 

## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.


---


# Ex. No : 4	
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
## Register Number : 212224240086
## Date : 

## AIM   
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.

## PROGRAM


## OUTPUT 

## RESULT
A  YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.


---


# Ex. No : 5	
# RECOGNITION OF THE GRAMMAR (a<sup>n</sup>b where n>=10) USING YACC
## Register Number : 212224240086
## Date : 

## AIM   
To write a YACC program to recognize the grammar a<sup>n</sup>b where n>=10.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
 
## PROGRAM


## OUTPUT 

## RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.


---


# Ex. No : 6	
# IMPLEMENTATION OF THE BACK END OF THE COMPILER 
## Register Number : 212224240086
## Date : 

## AIM   
To write a program to implement the back end of the compiler.

## ALGORITHM
1.	Start the program.
2.	Get the three variables from statements and stored in the text file k.txt.
3.	Compile the program and give the path of the source file.
4.	Execute the program.
5.	Target code for the given statement is produced.
6.	Stop the program.

## PROGRAM


## OUTPUT 

## RESULT
The back end of the compiler is implemented successfully, and the output is verified.
