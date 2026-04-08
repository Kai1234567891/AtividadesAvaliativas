Desafio 2
Implemente um programa em C que receba uma string e retorne essa string invertida utilizando uma pilha.

Requisitos
Implementar a pilha manualmente utilizando struct e alocação dinâmica.
Inserir cada caractere da string na pilha.
Utilizar a pilha para gerar a string invertida.
Restrições
Não utilizar funções prontas para inverter string.
Não utilizar vetor auxiliar para armazenar a string invertida.
Manipular apenas via operações da pilha.

Código:
#include <stdio.h>
#include <stdlib.h>


typedef struct No {
    char dado;
    struct No* prox;
} No;


typedef struct {
    No* topo;
} Pilha;


void inicializar(Pilha* p) {
    p->topo = NULL;
}


int estaVazia(Pilha* p) {
    return (p->topo == NULL);
}


void push(Pilha* p, char c) {
    No* novo = (No*) malloc(sizeof(No));
    if (novo == NULL) {
        printf("Erro de alocação!\n");
        exit(1);
    }
    novo->dado = c;
    novo->prox = p->topo;
    p->topo = novo;
}


char pop(Pilha* p) {
    if (estaVazia(p)) {
        printf("Pilha vazia!\n");
        exit(1);
    }
    No* temp = p->topo;
    char c = temp->dado;
    p->topo = temp->prox;
    free(temp);
    return c;
}

int main() {
    Pilha p;
    inicializar(&p);

    char str[100];

    printf("Digite uma string: ");
    fgets(str, sizeof(str), stdin);

   
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] != '\n') { 
            push(&p, str[i]);
        }
    }

    printf("String invertida: ");

   
    while (!estaVazia(&p)) {
        printf("%c", pop(&p));
    }

    printf("\n");

    return 0;
}

Explicação do Código:
#include <stdio.h>   // Biblioteca para entrada e saída (printf, fgets)
#include <stdlib.h>  // Biblioteca para alocação dinâmica (malloc, free, exit)

// Estrutura que representa um nó da pilha
typedef struct No {
    char dado;           // Armazena um caractere
    struct No* prox;     // Ponteiro para o próximo nó da pilha
} No;

// Estrutura da pilha
typedef struct {
    No* topo;            // Ponteiro para o topo da pilha
} Pilha;

// Inicializa a pilha (começa vazia)
void inicializar(Pilha* p) {
    p->topo = NULL;      // Define o topo como NULL
}

// Verifica se a pilha está vazia
int estaVazia(Pilha* p) {
    return (p->topo == NULL); // Retorna 1 se vazia, 0 caso contrário
}

// Função para empilhar um caractere (push)
void push(Pilha* p, char c) {

    // Aloca memória para um novo nó
    No* novo = (No*) malloc(sizeof(No));

    // Verifica se houve erro na alocação
    if (novo == NULL) {
        printf("Erro de alocação!\n");
        exit(1); // Encerra o programa
    }

    // Armazena o caractere no nó
    novo->dado = c;

    // O novo nó aponta para o topo atual da pilha
    novo->prox = p->topo;

    // Atualiza o topo da pilha para o novo nó
    p->topo = novo;
}

// Função para desempilhar um caractere (pop)
char pop(Pilha* p) {

    // Verifica se a pilha está vazia
    if (estaVazia(p)) {
        printf("Pilha vazia!\n");
        exit(1); // Encerra o programa
    }

    // Guarda o nó do topo
    No* temp = p->topo;

    // Guarda o caractere do topo
    char c = temp->dado;

    // Atualiza o topo para o próximo nó
    p->topo = temp->prox;

    // Libera a memória do nó removido
    free(temp);

    // Retorna o caractere removido
    return c;
}

int main() {

    Pilha p;              // Declara a pilha
    inicializar(&p);      // Inicializa a pilha

    char str[100];        // Vetor para armazenar a string digitada

    // Solicita ao usuário uma string
    printf("Digite uma string: ");

    // Lê a string (inclui o '\n' ao pressionar Enter)
    fgets(str, sizeof(str), stdin);

    // Percorre a string até o caractere final '\0'
    for (int i = 0; str[i] != '\0'; i++) {

        // Ignora o caractere de quebra de linha '\n'
        if (str[i] != '\n') {

            // Empilha cada caractere
            push(&p, str[i]);
        }
    }

    // Exibe mensagem de saída
    printf("String invertida: ");

    // Enquanto a pilha não estiver vazia
    while (!estaVazia(&p)) {

        // Desempilha e imprime cada caractere
        printf("%c", pop(&p));
    }

    // Quebra de linha ao final
    printf("\n");

    return 0; // Finaliza o programa
}
