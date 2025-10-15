# Ex-4-LETTER-FOLLOWED-BY-ANY-NUMBER-OF-LETTERS-OR-DIGITS-USING-YACC
# REGISTER NUMBER:2305001019
# Date:15.10.2025
# Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.
# PROGRAM
# expr4.l
~~~
%{
#include "y.tab.h"
#include <string.h>
%}

%%
[a-zA-Z][a-zA-Z0-9]*    { yylval.str = strdup(yytext); return IDENTIFIER; }
\n                      { return '\n'; }
.                       { return yytext[0]; }
%%

int yywrap() {
    return 1;
}
~~~

# expr4.y
~~~%{
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

extern int yylex();
void yyerror(const char *msg);

%}

%union {
    char *str;
}

%token <str> IDENTIFIER

%%
start:
    IDENTIFIER '\n' {
        printf("Valid variable: %s\n", $1);
        free($1);  // clean up strdup memory
    }
    ;
%%

int main() {
    printf("Enter a variable name:\n");
    return yyparse();
}

void yyerror(const char *msg) {
    printf("Invalid variable name\n");
}
~~~
# Output 
<img width="682" height="437" alt="Screenshot 2025-10-15 120432" src="https://github.com/user-attachments/assets/508609ec-319b-4e8c-a6af-520be14893e2" />

# Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.
