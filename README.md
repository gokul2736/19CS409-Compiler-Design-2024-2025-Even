## Compiler Design- All Exps

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
## Date : 10.03.2026

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
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
int isKeyword(char buffer[]) {
char keywords[5][10] = {"if", "else", "while", "for", "int"};
for (int i = 0; i < 5; ++i) {
if (strcmp(buffer, keywords[i]) == 0) {
return 1;
}
}
return 0;
}
int main() {
char ch;
char operators[] = "+-*/=;";
char buffer[15];
int i = 0;
printf("Enter your input :\n");
while ((ch = getchar()) != EOF) {
// Check if character is an operator
if (strchr(operators, ch) != NULL) {
// If there is something in the buffer, process it before the operator
if (i > 0) {
buffer[i] = '\0';
// Check if the buffer holds a keyword, identifier, or number
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
} else if (isdigit(buffer[0])) {
printf("Number: %s\n", buffer);
}
i = 0; // Reset buffer for next token
}
printf("Operator: %c\n", ch); // Output operator
} else if (isalnum(ch)) {
// Add alphanumeric character to buffer
if (i < 14) { // Avoid buffer overflow
buffer[i++] = ch;
}
} else if ((ch == ' ' || ch == '\n' || ch == '\t') && i > 0) {
// End of token, process it
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
} else if (isdigit(buffer[0])) {
printf("Number: %s\n", buffer);
}
i = 0; // Reset buffer
}
// If a digit follows a letter (e.g., 'b' followed by '1'), treat it as separa
if (i > 0 && isalpha(buffer[i-1]) && isdigit(ch)) {
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
}
// Reset buffer for the number token
i = 0;
buffer[i++] = ch; // Add digit to the buffer for number
}
}
// Process any remaining buffer at the end of input
if (i > 0) {
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
} else if (isdigit(buffer[0])) {
printf("Number: %s\n", buffer);
}
}
return 0;
}
```

## OUTPUT 
![image](https://github.com/user-attachments/assets/01340920-a8d5-4c48-98ff-ef44a62e6980)

## RESULT
The lexical analyzer is implemented using lex and the output is verified.


---


# Ex. No : 3	
# RECOGNITION OF A VALID ARITHMETIC EXPRESSION THAT USES
## Register Number : 212224240086
## Date : 12.03.2026

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
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

char expr[100];
int pos = 0;

int E();
int F();
void error();

int F() {
    if (isdigit(expr[pos])) {
        while (isdigit(expr[pos])) pos++;
        return 1;
    }
    else if (isalpha(expr[pos])) {
        while (isalnum(expr[pos])) pos++;
        return 1;
    }
    else if (expr[pos] == '(') {
        pos++;
        if (E()) {
            if (expr[pos] == ')') {
                pos++;
                return 1;
            }
        }
        return 0;
    }
    return 0;
}

int E() {
    if (!F()) return 0;
    while (expr[pos] == '+' || expr[pos] == '-' || expr[pos] == '*' || expr[pos] == '/') {
        pos++;
        if (!F())
            return 0;
    }
    return 1;
}

void error() {
    printf("\nError: Invalid arithmetic expression\n");
}

int main() {
    printf("Enter the expression:\n");
    fgets(expr, sizeof(expr), stdin);
    expr[strcspn(expr, "\n")] = '\0';
    pos = 0;
    if (E() && expr[pos] == '\0') {
        printf("\nValid arithmetic expression\n");
    } else {
        error();
    }
    return 0;
}

```

## OUTPUT 

<img width="450" height="323" alt="image" src="https://github.com/user-attachments/assets/cde9341e-7015-48ec-8cda-22d050b86249" />


## For Invalid Arithmetic Expression
<img width="499" height="397" alt="image" src="https://github.com/user-attachments/assets/7d3b58df-44f3-4af1-a52a-5ef8936e7f48" />


## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.


---


# Ex. No : 4	
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
## Register Number : 212224240086  
## Date : 10.03.2026

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
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

// List of reserved keywords
const char *keywords[] = {"int", "float", "double"};
int isKeyword(const char *str) {
    for (int i = 0; i < 3; i++) {
        if (strcmp(str, keywords[i]) == 0)
            return 1;
    }
    return 0;
}

// Function to check if variable name is valid
int isValidVariable(const char *str) {
    if (!isalpha(str[0])) // Must start with a letter
        return 0;

    for (int i = 1; str[i] != '\0'; i++) {
        if (!isalnum(str[i])) // Only letters and digits allowed
            return 0;
    }

    if (isKeyword(str)) // Should not be a keyword
        return 0;

    return 1;
}

int main() {
    char var[100];
    printf("Enter a variable name: ");
    scanf("%s", var);

    if (isValidVariable(var))
        printf("Valid variable name.\n");
    else
        printf("Invalid variable name.\n");

    return 0;
}
```

## OUTPUT 
<img width="488" height="319" alt="image" src="https://github.com/user-attachments/assets/fee09e90-4a25-4c23-944a-881db46ed7d3" />

## RESULT
A  YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.




---


# Ex. No : 5	
# RECOGNITION OF THE GRAMMAR (a<sup>n</sup>b where n>=10) USING YACC
## Register Number : 212224240086
## Date : 12.03.2026

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
f4.l
```
%{
/* Definition section */
#include "y.tab.h"
%}

/* Rule Section */
%%
[aA]        { return A; }
[bB]        { return B; }
\n          { return NL; }
.           { return yytext[0]; }
%%

int yywrap(void)
{
    return 1;
}
```
f4.y
```
%{
#include <stdio.h>
#include <stdlib.h>

int yylex(void);
void yyerror(const char *msg);
%}

/* Declare tokens */
%token A B NL

%%
/* Grammar rules */

stmt: S NL               { printf("valid string\n"); exit(0); }
    ;

S: A S B                 /* a matched pair of A and B, possibly nested */
 |                       /* empty (epsilon) */
    ;
%%

int main(void)
{
    printf("enter the string\n");
    yyparse();
    return 0;
}

void yyerror(const char *msg)
{
    printf("invalid string\n");
    exit(0);
}

```
## OUTPUT 
<img width="607" height="165" alt="Screenshot from 2025-10-25 15-11-26" src="https://github.com/user-attachments/assets/98218741-debc-41ad-9c27-8fbd5e81eaa9" />

## RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.


---


# Ex. No : 6	
# IMPLEMENTATION OF THE BACK END OF THE COMPILER 
## Register Number : 212224240086
## Date : 10.03.2026

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
p.c
```
#include <stdio.h> 
#include <ctype.h> 
#include <stdlib.h>

int main() {
int i = 2, j = 0, k = 2, k1 = 0; char ip[10], kk[10];
FILE *fp;

printf("Enter the filename of the intermediate code: "); scanf("%s", kk);

fp = fopen(kk, "r"); if (fp == NULL) {
printf("\nError in opening the file\n"); return 1;
}
printf("\nStatement\tTarget Code\n\n"); while (fscanf(fp, "%s", ip) != EOF) {
printf("%s\tMOV %c,R%d SUB ", ip, ip[i + k], j);

if (ip[i + 1] == '+')
printf("ADD "); else
printf("SUB ");

if (islower(ip[i])) printf("%c,R%d\n", ip[i + k1], j);
else
printf("%c,%c\n", ip[i], ip[i + 2]);

j++;
k1 = 2;
k = 0;
}

fclose(fp);
return 0;
}
```
p.txt
```
X=a-b 
Y=a-c 
Z=a+b 
C=a-b 
C=a-b

```
## OUTPUT 
<img width="480" height="270" alt="Screenshot from 2025-10-25 16-05-08" src="https://github.com/user-attachments/assets/cb49cde7-b834-42f6-a627-f7588b07d052" />

## RESULT
The back end of the compiler is implemented successfully, and the output is verified.


## OUTPUT 

## RESULT
The back end of the compiler is implemented successfully, and the output is verified.
