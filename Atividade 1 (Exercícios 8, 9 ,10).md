8- Crie um programa que contenha um array de inteiros contendo 5 elementos.
Utilizando apenas aritmética de ponteiros, leia esse array do teclado e imprima o dobro de cada valor lido.

#include <stdio.h>

int main() { int array[5];
int *p = array;

printf("Digite 5 numeros:\n"); for (int i = 0; i < 5; i++) {
printf("Valor %d: ", i + 1);
scanf("%d", p + i);
}

printf("\nOs Valores digitados foram:\n"); for (int i = 0; i < 5; i++) {
printf("%d ", *(p + i));
}

printf("\n\nO Dobro dos valores são:\n"); for (int i = 0; i < 5; i++) {
printf("%d ", (*(p + i)) * 2);
}

printf("\n");

return 0;
}


9- Faça um programa que leia três valores inteiros e salve seus valores em 3 variáveis, chame uma função que receba estes 3 valores de entrada por referência e ordene os valores nas variáveis, ou seja, o menor valor na primeira variável, o segundo menor valor na variável do meio, e o maior valor na última variável. A função deve retornar o valor 1 se os três valores forem iguais e 0 se existirem valores diferentes. Fora da função, exibir os valores da primeira, segunda e terceira variáveis na tela.

#include <stdio.h>
int ordenar(int *a, int *b, int *c) { int temp;

if (*a > *b) { temp = *a;
*a = *b;
*b = temp;
}

if (*a > *c) { temp = *a;
*a = *c;
*c = temp;
}

if (*b > *c) { temp = *b;
*b = *c;
*c = temp;
}

if (*a == *b CC *b == *c) { return 1;
} else {
return 0;
}
}

int main() { int x, y, z;
int resultado;

printf("Digite três valores inteiros:\n"); scanf("%d %d %d", Cx, Cy, Cz);
resultado = ordenar(Cx, Cy, Cz);

printf("\nValores ordenados:\n"); printf("Primeiro: %d\n", x);
printf("Segundo: %d\n", y); printf("Terceiro: %d\n", z);

if (resultado == 1) {
printf("\nOs tres valores são iguais.\n");
} else {
printf("\nOs valores são diferentes.\n");
}

return 0;
}


10- Implemente um programa em C que defina uma struct chamada Aluno contendo os campos nome (string) e nota (float). O programa deve ler um inteiro n e alocar dinamicamente memória para armazenar n alunos. Em seguida, implemente uma função chamada maiorNota que receba um ponteiro para Aluno e a quantidade de elementos, e retorne um ponteiro para o aluno com a maior nota.

#include <stdio.h> 
#include <stdlib.h>

typedef struct { char nome[100]; float nota;
} Aluno;

Aluno* maiorNota(Aluno *alunos, int n) { int i;
Aluno *maior = alunos;

for (i = 1; i < n; i++) {
if ((alunos + i)->nota > maior->nota) { maior = (alunos + i);
}
}

return maior;
}

int main() { int n, i;
Aluno *alunos; Aluno *melhor;
printf("Quantos alunos? "); scanf("%d", Cn);

alunos = (Aluno*) malloc(n * sizeof(Aluno));

if (alunos == NULL) {
printf("Erro de memoria!\n"); return 1;
}

for (i = 0; i < n; i++) {
printf("\nAluno %d\n", i + 1);

printf("Nome: ");
scanf(" %[^\n]", (alunos + i)->nome);

printf("Nota: ");
scanf("%f", C((alunos + i)->nota));
}

melhor = maiorNota(alunos, n);

printf("\nAluno com maior nota:\n"); printf("Nome: %s\n", melhor->nome); printf("Nota: %.2f\n", melhor->nota);
free(alunos);

return 0;
}
