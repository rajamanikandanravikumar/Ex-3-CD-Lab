# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:07-05-2025
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM:
```
%{
#include "ss.tab.h"
#include <stdlib.h>
#include <stdio.h>
%}

%%

[0-9]+          { yylval = atoi(yytext); return NUMBER; }
[a-zA-Z]        { printf("Identifier is %s\n", yytext); return ID; }
"="             { printf("Operator is EQUAL\n"); return '='; }
"+"             { printf("Operator is PLUS\n"); return '+'; }
"-"             { printf("Operator is MINUS\n"); return '-'; }
"*"             { printf("Operator is MULTIPLY\n"); return '*'; }
"/"             { printf("Operator is DIVIDE\n"); return '/'; }
"%"             { printf("Operator is MODULO\n"); return '%'; }
[ \t]           ; // ignore whitespace
[\n]            return '\n';
.               return yytext[0];

%%

int yywrap() {
    return 1;
}


```
```
%{
#include <stdio.h>
#include <stdlib.h>

int yylex(void);
void yyerror(const char *s);
%}

%token NUMBER ID

%left '='
%left '+' '-'
%left '*' '/' '%'

%%

input:
    | input expr '\n'   { printf("Valid arithmetic expression\n"); }
    ;

expr:
      ID '=' expr
    | expr '+' expr
    | expr '-' expr
    | expr '*' expr
    | expr '/' expr
    | expr '%' expr
    | '(' expr ')'
    | NUMBER
    | ID
    ;

%%

void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

int main() {
    printf("Enter an arithmetic expression:\n");
    yyparse();
    return 0;
}

```
# OUTPUT:
![image](https://github.com/user-attachments/assets/a0448c27-057f-47ff-8efe-77a921b66a7a)


# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
