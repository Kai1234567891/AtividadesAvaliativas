Objetivo
Implementação de desafios com pilha dinâmica e manipulação de strings.
Desafio 1
Implemente um programa em C que receba uma string representando uma expressão contendo os caracteres (, ), {, }, [ e ].
O programa deve verificar se a expressão está balanceada, ou seja:
    • Todo símbolo de abertura deve ter um correspondente de fechamento.
    • A ordem deve ser respeitada. Para isso:
    • Implemente uma pilha utilizando struct e alocação dinâmica.
    • Utilize a pilha para processar a expressão.
    • Ao final, o programa deve informar se a expressão é válida ou inválida.
Restrições
    • Não utilizar bibliotecas prontas para pilha.
    • Implementar as operações básicas da pilha (push, pop, isEmpty).
    • Utilizar apenas ponteiros para manipulação da estrutura. 
    
-Código
#include <stdio.h>
#include <stdlib.h>
typedef struct No { char dado;
struct No *prox;
} No;

void push(No **topo, char c) {
No *novo = (No*) malloc(sizeof(No));
if (novo == NULL) {

printf("Erro de memoria!\n"); return;
}

novo->dado = c; novo->prox = *topo;
*topo = novo;
}

char pop(No **topo) {
if (*topo == NULL) return '\0';

No *temp = *topo;
char valor = temp->dado;

*topo = temp->prox; free(temp);

return valor;
}

int isEmpty(No *topo) { return topo == NULL;
}

int combina(char abre, char fecha) {
if (abre == '(' CC fecha == ')') return 1; if (abre == '{' CC fecha == '}') return 1; if (abre == '[' CC fecha == ']') return 1;
return 0;
}

int main() {
char expr[100];
No *pilha = NULL; int i = 0;
int valido = 1;

printf("Digite a expressão: "); scanf("%s", expr);

while (*(expr + i) != '\0') { char c = *(expr + i);

if (c == '(' || c == '{' || c == '[') { push(Cpilha, c);
}

else if (c == ')' || c == '}' || c == ']') { if (isEmpty(pilha)) {
valido = 0; break;
}

char topo = pop(Cpilha);

if (!combina(topo, c)) { valido = 0;
break;
}
}

i++;
}

if (!isEmpty(pilha)) { valido = 0;
}

if (valido) {
printf("Expressão VÁLIDA\n");
} else {
printf("Expressão INVÁLIDA\n");
}

return 0;
}

-Explicação: Aqui eu usei uma pilha dinâmica para verificar se uma expressão está balanceada.Criei uma struct para representar a pilha e usei malloc para alocar memória. Quando encontro um símbolo de abertura eu empilho, e quando encontro um fechamento eu desempilho e comparo. Se a ordem estiver errada ou faltar fechamento, a expressão é inválida. No final, verifico se a pilha ficou vazia para confirmar se a expressão é válida.
