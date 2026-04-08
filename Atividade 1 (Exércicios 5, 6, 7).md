5-Faça um programa que lê um vetor de 3 elementos e uma matriz de 3 x 3 elementos. Em seguida, o programa deve fazer a multiplicação do vetor pelas colunas da matriz. 
-Código:
#include <stdio.h>
int main() {
    int vetor[3], matriz[3][3];
    int resultado[3] = {0, 0, 0};

   printf("Digite os 3 elementos do vetor:\n");
    for (int i = 0; i < 3; i++) {
        scanf("%d", &vetor[i]);
    }

   printf("Digite os elementos da matriz 3x3:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            scanf("%d", &matriz[i][j]);
        }
    }

  for (int j = 0; j < 3; j++) {
        for (int i = 0; i < 3; i++) {
            resultado[j] += vetor[i] * matriz[i][j];
        }
    }

  printf("Resultado da multiplicacao:\n");
    for (int i = 0; i < 3; i++) {
        printf("%d ", resultado[i]);
    }

    printf("\n");
    
    return 0;
}
-Explicação: Aqui eu li um vetor de 3 posições e uma matriz 3x3. Depois fiz a multiplicação do vetor pelas colunas da matriz. Usei dois laços para percorrer os valores e fazer os cálculos.
O resultado é armazenado em outro vetor. No final, mostro o resultado da multiplicação.



6-Faça um programa que leia os dados de 10 alunos (Nome, matrícula, Média Final) usando struct, armazenando em um vetor. Uma vez lidos os dados, divida estes dados em 2 novos vetores, o vetor dos aprovados e o vetor dos reprovados, considerando a média mínima para a aprovação como sendo 5.0. Exibir na tela os dados do vetor de aprovados, seguido dos dados do vetor de reprovados.
-Código:
#include <stdio.h>
#include <string.h>

struct Aluno {
    char nome[50];
    int matricula;
    float media;
};

int main() {
    struct Aluno alunos[10];
    struct Aluno aprovados[10];
    struct Aluno reprovados[10];

    int contAprovados = 0, contReprovados = 0;

    for (int i = 0; i < 10; i++) {
        printf("\nAluno %d\n", i + 1);

        printf("Nome: ");
        scanf(" %[^\n]", alunos[i].nome);

        printf("Matricula: ");
        scanf("%d", &alunos[i].matricula);

        printf("Media final: ");
        scanf("%f", &alunos[i].media);

        if (alunos[i].media >= 5.0) {
            aprovados[contAprovados] = alunos[i];
            contAprovados++;
        } else {
            reprovados[contReprovados] = alunos[i];
            contReprovados++;
        }
    }

  printf("\n--- ALUNOS APROVADOS ---\n");
    for (int i = 0; i < contAprovados; i++) {
        printf("\nNome: %s", aprovados[i].nome);
        printf("\nMatricula: %d", aprovados[i].matricula);
        printf("\nMedia: %.2f\n", aprovados[i].media);
    }

  printf("\n--- ALUNOS REPROVADOS ---\n");
    for (int i = 0; i < contReprovados; i++) {
        printf("\nNome: %s", reprovados[i].nome);
        printf("\nMatricula: %d", reprovados[i].matricula);
        printf("\nMedia: %.2f\n", reprovados[i].media);
    }

    return 0;
}
-Explicação: Aqui eu usei uma struct para guardar os dados dos alunos (nome, matrícula e média). Li os dados de 10 alunos e armazenei em um vetor. Depois separei os alunos em dois vetores: aprovados e reprovados, usando a média 5.0 como base.
Usei contadores para controlar quantos alunos foram para cada grupo. No final, mostro primeiro os aprovados e depois os reprovados.



7-Faça um programa que leia um vetor com dados de 5 livros usando struct: título (máximo 30 letras), autor (máximo 15 letras) e ano. Procure um livro por título, perguntando ao usuário qual título deseja buscar. Mostre os dados de todos os livros encontrados.
-Código
#include <stdio.h>
#include <string.h>

struct Livro {
    char titulo[31];
    char autor[16];
    int ano;
};

int main() {
    struct Livro livros[5];
    char busca[31];
    int encontrado = 0;

for (int i = 0; i < 5; i++) {
        printf("\nLivro %d\n", i + 1);

        printf("Titulo: ");
        scanf(" %[^\n]", livros[i].titulo);

        printf("Autor: ");
        scanf(" %[^\n]", livros[i].autor);

        printf("Ano: ");
        scanf("%d", &livros[i].ano);
    }

printf("\nDigite o titulo que deseja buscar: ");
    scanf(" %[^\n]", busca);

  for (int i = 0; i < 5; i++) {
        if (strcmp(livros[i].titulo, busca) == 0) {
            printf("\n--- Livro encontrado ---\n");
            printf("Titulo: %s\n", livros[i].titulo);
            printf("Autor: %s\n", livros[i].autor);
            printf("Ano: %d\n", livros[i].ano);
            encontrado = 1;
        }
    }

  if (!encontrado) {
        printf("\nNenhum livro encontrado com esse titulo.\n");
    }

    return 0;
}
-Explicação: Aqui eu usei uma struct para guardar os dados dos livros (título, autor e ano). Li os dados de 5 livros e armazenei em um vetor. Depois pedi para o usuário digitar um título para buscar. Usei strcmp para comparar os títulos e verificar se são iguais.
Se encontrar, mostro os dados do livro.Se não encontrar nenhum, aviso que não foi encontrado.
