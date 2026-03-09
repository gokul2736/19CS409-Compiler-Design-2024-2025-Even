# EX:01
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
