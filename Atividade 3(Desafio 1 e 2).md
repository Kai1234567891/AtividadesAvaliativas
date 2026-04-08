Desafio 1
Implemente um programa em C que simule o atendimento de uma fila de clientes.

Cada cliente deve ser representado por uma struct contendo:

id (int)
tempoAtendimento (int, em minutos)
O programa deve:

Ler um número n de clientes.
Inserir os clientes em uma fila (ordem de chegada).
Simular o atendimento sequencial, exibindo:
id do cliente atendido.
tempo de espera até ser atendido.
Regras:

O tempo de espera de um cliente é a soma dos tempos de atendimento de todos os clientes à sua frente.
Para isso:

Implemente uma fila utilizando struct e ponteiros.
Crie operações de enqueue e dequeue.
Restrições
Não utilizar vetores para simular a fila.
Não utilizar bibliotecas prontas.
Toda a estrutura deve ser dinâmica (malloc/free).

Código:
#include <stdio.h>
#include <stdlib.h>


typedef struct Cliente {
    int id;
    int tempoAtendimento;
    struct Cliente* prox;
} Cliente;


typedef struct {
    Cliente* inicio;
    Cliente* fim;
} Fila;


void inicializar(Fila* f) {
    f->inicio = NULL;
    f->fim = NULL;
}


int estaVazia(Fila* f) {
    return (f->inicio == NULL);
}


void enqueue(Fila* f, int id, int tempo) {
    Cliente* novo = (Cliente*) malloc(sizeof(Cliente));
    if (novo == NULL) {
        printf("Erro de alocação!\n");
        exit(1);
    }

    novo->id = id;
    novo->tempoAtendimento = tempo;
    novo->prox = NULL;

    if (estaVazia(f)) {
        f->inicio = novo;
        f->fim = novo;
    } else {
        f->fim->prox = novo;
        f->fim = novo;
    }
}


Cliente* dequeue(Fila* f) {
    if (estaVazia(f)) {
        return NULL;
    }

    Cliente* temp = f->inicio;
    f->inicio = temp->prox;

    if (f->inicio == NULL) {
        f->fim = NULL;
    }

    return temp;
}

int main() {
    Fila fila;
    inicializar(&fila);

    int n;

    printf("Digite o número de clientes: ");
    scanf("%d", &n);

    
    for (int i = 0; i < n; i++) {
        int id, tempo;
        printf("Cliente %d - ID: ", i + 1);
        scanf("%d", &id);
        printf("Cliente %d - Tempo de atendimento: ", i + 1);
        scanf("%d", &tempo);

        enqueue(&fila, id, tempo);
    }

    printf("\nSimulação de atendimento:\n");

    int tempoEspera = 0;

    
    while (!estaVazia(&fila)) {
        Cliente* c = dequeue(&fila);

        printf("Cliente ID: %d\n", c->id);
        printf("Tempo de espera: %d minutos\n\n", tempoEspera);

        tempoEspera += c->tempoAtendimento;

        free(c);
    }

    return 0;
}

Explicação do código:
#include <stdio.h>   // Biblioteca para entrada e saída (printf, scanf)
#include <stdlib.h>  // Biblioteca para alocação dinâmica (malloc, free, exit)

// Estrutura que representa um cliente
typedef struct Cliente {
    int id;                     // Identificador do cliente
    int tempoAtendimento;       // Tempo de atendimento em minutos
    struct Cliente* prox;       // Ponteiro para o próximo cliente na fila
} Cliente;

// Estrutura da fila
typedef struct {
    Cliente* inicio;            // Aponta para o primeiro cliente da fila
    Cliente* fim;               // Aponta para o último cliente da fila
} Fila;

// Inicializa a fila (vazia)
void inicializar(Fila* f) {
    f->inicio = NULL;           // Nenhum elemento no início
    f->fim = NULL;              // Nenhum elemento no fim
}

// Verifica se a fila está vazia
int estaVazia(Fila* f) {
    return (f->inicio == NULL); // Se início é NULL, fila está vazia
}

// Função para inserir cliente na fila (enqueue)
void enqueue(Fila* f, int id, int tempo) {

    // Aloca memória para um novo cliente
    Cliente* novo = (Cliente*) malloc(sizeof(Cliente));

    // Verifica erro de alocação
    if (novo == NULL) {
        printf("Erro de alocação!\n");
        exit(1);
    }

    // Preenche os dados do cliente
    novo->id = id;
    novo->tempoAtendimento = tempo;

    // Como será o último da fila, aponta para NULL
    novo->prox = NULL;

    // Se a fila estiver vazia
    if (estaVazia(f)) {

        // O novo cliente será o primeiro e o último
        f->inicio = novo;
        f->fim = novo;

    } else {
        // Liga o último cliente atual ao novo
        f->fim->prox = novo;

        // Atualiza o fim da fila
        f->fim = novo;
    }
}

// Função para remover cliente da fila (dequeue)
Cliente* dequeue(Fila* f) {

    // Se a fila estiver vazia, retorna NULL
    if (estaVazia(f)) {
        return NULL;
    }

    // Guarda o primeiro cliente
    Cliente* temp = f->inicio;

    // Avança o início para o próximo cliente
    f->inicio = temp->prox;

    // Se a fila ficou vazia após remoção
    if (f->inicio == NULL) {
        f->fim = NULL; // Atualiza o fim também
    }

    // Retorna o cliente removido (não libera ainda)
    return temp;
}

int main() {

    Fila fila;                 // Declara a fila
    inicializar(&fila);        // Inicializa a fila

    int n;                     // Quantidade de clientes

    // Solicita quantidade de clientes
    printf("Digite o número de clientes: ");
    scanf("%d", &n);

    // Loop para inserir os clientes na fila
    for (int i = 0; i < n; i++) {
        int id, tempo;

        // Lê o ID do cliente
        printf("Cliente %d - ID: ", i + 1);
        scanf("%d", &id);

        // Lê o tempo de atendimento
        printf("Cliente %d - Tempo de atendimento: ", i + 1);
        scanf("%d", &tempo);

        // Insere o cliente na fila
        enqueue(&fila, id, tempo);
    }

    // Mensagem inicial da simulação
    printf("\nSimulação de atendimento:\n");

    int tempoEspera = 0; // Acumula o tempo de espera

    // Enquanto houver clientes na fila
    while (!estaVazia(&fila)) {

        // Remove o próximo cliente da fila
        Cliente* c = dequeue(&fila);

        // Exibe o ID do cliente atendido
        printf("Cliente ID: %d\n", c->id);

        // Exibe o tempo que ele esperou
        printf("Tempo de espera: %d minutos\n\n", tempoEspera);

        // Atualiza o tempo de espera para o próximo cliente
        tempoEspera += c->tempoAtendimento;

        // Libera a memória do cliente atendido
        free(c);
    }

    return 0; // Finaliza o programa
}

Desafio 2
Implemente um sistema de fila de impressão onde cada documento possui:

id (int)
número de páginas (int)
prioridade (int, quanto menor o valor, maior a prioridade)
O programa deve:

Inserir documentos na fila.
Sempre atender primeiro o documento de maior prioridade.
Em caso de empate, respeitar a ordem de chegada.
Requisitos
Implementar a fila manualmente.
Garantir a ordenação por prioridade no momento da inserção ou remoção.
Restrições
Não utilizar estruturas prontas.
Não ordenar usando funções externas (ex: qsort).

Código:
#include <stdio.h>
#include <stdlib.h>

typedef struct Documento {
    int id;
    int paginas;
    int prioridade;
    struct Documento* prox;
} Documento;

typedef struct {
    Documento* inicio;
} Fila;

void inicializar(Fila* f) {
    f->inicio = NULL;
}

int estaVazia(Fila* f) {
    return (f->inicio == NULL);
}

void enqueue(Fila* f, int id, int paginas, int prioridade) {
    Documento* novo = (Documento*) malloc(sizeof(Documento));
    if (novo == NULL) {
        printf("Erro de alocação!\n");
        exit(1);
    }

    novo->id = id;
    novo->paginas = paginas;
    novo->prioridade = prioridade;
    novo->prox = NULL;

    
    if (estaVazia(f) || prioridade < f->inicio->prioridade) {
        novo->prox = f->inicio;
        f->inicio = novo;
    } else {
        Documento* atual = f->inicio;

        while (atual->prox != NULL &&
               atual->prox->prioridade <= prioridade) {
            atual = atual->prox;
        }

        novo->prox = atual->prox;
        atual->prox = novo;
    }
}

Documento* dequeue(Fila* f) {
    if (estaVazia(f)) {
        return NULL;
    }

    Documento* temp = f->inicio;
    f->inicio = temp->prox;
    return temp;
}

int main() {
    Fila fila;
    inicializar(&fila);

    int n;

    printf("Digite o número de documentos: ");
    scanf("%d", &n);

   
    for (int i = 0; i < n; i++) {

        
        printf("Inserindo documento %d...\n", i + 1);

        int id, paginas, prioridade;

        printf("\nDocumento %d\n", i + 1);

        printf("ID: ");
        scanf("%d", &id);

        printf("Número de páginas: ");
        scanf("%d", &paginas);

        printf("Prioridade (menor = mais urgente): ");
        scanf("%d", &prioridade);

        enqueue(&fila, id, paginas, prioridade);
    }

    printf("\nOrdem de impressão:\n");

   
    while (!estaVazia(&fila)) {
        Documento* doc = dequeue(&fila);

        printf("ID: %d | Páginas: %d | Prioridade: %d\n",
               doc->id, doc->paginas, doc->prioridade);

        free(doc);
    }

    return 0;
}

Explicação do Código:
#include <stdio.h>   // Biblioteca para entrada e saída (printf, scanf)
#include <stdlib.h>  // Biblioteca para alocação dinâmica (malloc, free, exit)

// Estrutura que representa um documento da fila de impressão
typedef struct Documento {
    int id;                     // Identificador do documento
    int paginas;                // Número de páginas do documento
    int prioridade;             // Prioridade (quanto menor, mais urgente)
    struct Documento* prox;     // Ponteiro para o próximo documento
} Documento;

// Estrutura da fila
typedef struct {
    Documento* inicio;          // Ponteiro para o primeiro elemento da fila
} Fila;

// Inicializa a fila (começa vazia)
void inicializar(Fila* f) {
    f->inicio = NULL;           // Nenhum elemento na fila
}

// Verifica se a fila está vazia
int estaVazia(Fila* f) {
    return (f->inicio == NULL); // Retorna 1 se estiver vazia, 0 caso contrário
}

// Função para inserir documento na fila com ordenação por prioridade
void enqueue(Fila* f, int id, int paginas, int prioridade) {

    // Aloca memória para um novo documento
    Documento* novo = (Documento*) malloc(sizeof(Documento));

    // Verifica se houve erro na alocação
    if (novo == NULL) {
        printf("Erro de alocação!\n");
        exit(1); // Encerra o programa
    }

    // Atribui os dados ao novo documento
    novo->id = id;
    novo->paginas = paginas;
    novo->prioridade = prioridade;

    // Inicialmente não aponta para ninguém
    novo->prox = NULL;

    // Caso 1: fila vazia OU nova prioridade é maior (menor número)
    if (estaVazia(f) || prioridade < f->inicio->prioridade) {

        // Insere no início da fila
        novo->prox = f->inicio;
        f->inicio = novo;

    } else {

        // Percorre a fila para encontrar a posição correta
        Documento* atual = f->inicio;

        // Avança enquanto:
        // - não chegou ao final
        // - próxima prioridade é menor ou igual (mantém ordem de chegada)
        while (atual->prox != NULL &&
               atual->prox->prioridade <= prioridade) {
            atual = atual->prox;
        }

        // Insere o novo documento na posição correta
        novo->prox = atual->prox;
        atual->prox = novo;
    }
}

// Função para remover o primeiro documento da fila
Documento* dequeue(Fila* f) {

    // Se a fila estiver vazia, retorna NULL
    if (estaVazia(f)) {
        return NULL;
    }

    // Guarda o primeiro documento
    Documento* temp = f->inicio;

    // Avança o início para o próximo elemento
    f->inicio = temp->prox;

    // Retorna o documento removido (não libera ainda)
    return temp;
}

int main() {

    Fila fila;                  // Declara a fila
    inicializar(&fila);         // Inicializa a fila

    int n;                      // Número de documentos

    // Solicita a quantidade de documentos
    printf("Digite o número de documentos: ");
    scanf("%d", &n);

    // Loop para inserir documentos na fila
    for (int i = 0; i < n; i++) {

        // Mensagem de debug para verificar o loop
        printf("Inserindo documento %d...\n", i + 1);

        int id, paginas, prioridade;

        // Exibe qual documento está sendo inserido
        printf("\nDocumento %d\n", i + 1);

        // Lê o ID
        printf("ID: ");
        scanf("%d", &id);

        // Lê o número de páginas
        printf("Número de páginas: ");
        scanf("%d", &paginas);

        // Lê a prioridade
        printf("Prioridade (menor = mais urgente): ");
        scanf("%d", &prioridade);

        // Insere o documento na fila
        enqueue(&fila, id, paginas, prioridade);
    }

    // Exibe a ordem de impressão
    printf("\nOrdem de impressão:\n");

    // Enquanto houver documentos na fila
    while (!estaVazia(&fila)) {

        // Remove o próximo documento (maior prioridade)
        Documento* doc = dequeue(&fila);

        // Exibe os dados do documento
        printf("ID: %d | Páginas: %d | Prioridade: %d\n",
               doc->id, doc->paginas, doc->prioridade);

        // Libera a memória do documento removido
        free(doc);
    }

    return 0; // Finaliza o programa
}
