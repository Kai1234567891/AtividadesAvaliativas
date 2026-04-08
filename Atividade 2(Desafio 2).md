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

Explicação do código:

#include <stdio.h>   // Biblioteca para entrada e saída (printf, fgets)
#include <stdlib.h>  // Biblioteca para alocação dinâmica (malloc, free, exit)

// Definição do nó da pilha
typedef struct No {
    char dado;           // Armazena um caractere
    struct No* prox;     // Ponteiro para o próximo nó
} No;

// Definição da pilha
typedef struct {
    No* topo;            // Ponteiro para o topo da pilha
} Pilha;

// Inicializa a pilha (topo começa como NULL)
void inicializar(Pilha* p) {
    p->topo = NULL;
}

// Verifica se a pilha está vazia
int estaVazia(Pilha* p) {
    return (p->topo == NULL);
}

// Função para inserir (empilhar) um caractere na pilha
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

    // O novo nó aponta para o topo atual
    novo->prox = p->topo;

    // Atualiza o topo da pilha para o novo nó
    p->topo = novo;
}

// Função para remover (desempilhar) um caractere da pilha
char pop(Pilha* p) {
    // Verifica se a pilha está vazia
    if (estaVazia(p)) {
        printf("Pilha vazia!\n");
        exit(1); // Encerra o programa
    }

    // Guarda o nó do topo
    No* temp = p->topo;

    // Guarda o valor do topo para retornar
    char c = temp->dado;

    // Atualiza o topo para o próximo nó
    p->topo = temp->prox;

    // Libera a memória do nó removido
    free(temp);

    // Retorna o caractere removido
    return c;
}

int main() {
    Pilha p;                  // Declara a pilha
    inicializar(&p);          // Inicializa a pilha

    char str[100];            // Vetor para armazenar a string digitada

    // Solicita a entrada do usuário
    printf("Digite uma string: ");

    // Lê a string (inclui o '\n' ao pressionar Enter)
    fgets(str, sizeof(str), stdin);

    // Percorre a string até encontrar o fim ('\0')
    for (int i = 0; str[i] != '\0'; i++) {

        // Ignora o caractere de quebra de linha '\n'
        if (str[i] != '\n') {

            // Empilha cada caractere
            push(&p, str[i]);
        }
    }

    // Exibe o início da saída
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
