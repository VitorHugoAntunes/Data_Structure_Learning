# 4 - Listas ligadas (linked lists)

Explore listas ligadas simples e duplamente ligadas, compreendendo suas características e operações.

## Definição

Estrutura de dados de tamanho variável, que crescem e diminuem de acordo com a necessidade. Cada novo elemento na lista é alocado dinamicamente na memória e podem ser modeladas como pilhas, filas e outras estruturas.

Operações típicas de uma lista ligada ou encadeada:

- Adicionar elementos ao final da lista;
- Remover elementos em determinado índice;
- Remover último elemento;
- Contar o número de elementos;
- Adicionar elementos em determinado índice.

A lista encadeada contém uma propriedade chamada `head` que serve para indicar o primeiro elemento da lista, contendo os valores do elemento atual e um ponteiro `next` para o próximo elemento da lista.

`Node` é uma representação de um elemento na lista, e seu papel é armazenar o valor desse elemento `data` e um ponteiro para o próximo elemento na sequência `next`.

**Estrutura do Nó (Node) para representar um elemento na lista encadeada:**

```c
typedef struct Node {
    int data;            // Valor do elemento
    struct Node* next;   // Ponteiro para o próximo elemento na sequência
} Node;
```

Primeiro, criamos um ponteiro para cada `node` que é um elemento da nossa lista, que carregará o seu valor e outro ponteiro apontando para o próximo da lista (pode ser `null`).

**Estrutura da lista com cabeça (LinkedList):**

```c
typedef struct {
    Node* head;   // Ponteiro para o primeiro nó na lista
    int size;     // Número de elementos na lista
} LinkedList;
```

A lista em si carrega consigo um ponteiro de um nó (elemento da lista) e o seu tamanho.

**Função para criar uma nova lista vazia:**

```c
LinkedList* createList() {
    LinkedList* list = (LinkedList*)malloc(sizeof(LinkedList));  // Aloca memória para a lista
    if (list == NULL) {  // Verifica se a alocação foi bem-sucedida
        perror("Erro ao alocar memória para a lista");  // Imprime mensagem de erro
        exit(EXIT_FAILURE);  // Encerra o programa indicando falha
    }
    list->head = NULL;  // Inicializa o ponteiro para o primeiro nó como NULL
    list->size = 0;     // Inicializa o número de elementos como zero
    return list;
}
```

Para criar uma lista, alocamos memória para ela se ela não for nula e iniciamos com tamanho e primeiro elemento nulo.

**Função para adicionar um elemento no final da lista:**

```c
void append(LinkedList* list, int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));  // Aloca memória para um novo nó
    if (newNode == NULL) {  // Verifica se a alocação foi bem-sucedida
        perror("Erro ao alocar memória para o novo nó");  // Imprime mensagem de erro
        exit(EXIT_FAILURE);  // Encerra o programa indicando falha
    }
    newNode->data = value;   // Define o valor do novo nó
    newNode->next = NULL;    // Inicializa o ponteiro para o próximo nó como NULL

    if (list->head == NULL) {
        list->head = newNode;  // Se a lista estiver vazia, o novo nó é o primeiro
    } else {
        Node* current = list->head;
        while (current->next != NULL) {
            current = current->next;  // Encontra o último nó na lista
        }
        current->next = newNode;  // Adiciona o novo nó ao final da lista
    }

    list->size++;  // Incrementa o número de elementos na lista
}
```

Para criar um novo elemento e adicionar na lista, alocamos memória para este novo valor e passamos o valor dele para a lista e depois verificamos se ele será o primeiro ou o próximo elemento da lista, e por fim incrementamos o tamanho da lista.

**Função para imprimir a lista com o tamanho de cada item e o tamanho total da lista em bytes:**

```c
void printList(LinkedList* list) {
    Node* current = list->head;
   size_t totalSize = 0;
    while (current != NULL) {
        printf("%d (Tamanho: %zu bytes) -> ", current->data, sizeof(current->data));
      
				printf("%p (Tamanho next: %zu bytes) -> ", (void *)current->next, sizeof(current->next));

				totalSize += sizeof(Node);
        current = current->next;
    }
    printf("NULL\n");

  printf("Tamanho total da lista: %zu bytes\n", totalSize);
}
```

Neste caso, para o tamanho da lista, é levado em consideração o tamanho de cada elemento somado com sua propriedade `next`, ou seja, cada elemento contém seu próprio valor e um ponteiro para o próximo elemento. Por exemplo: temos um Node atual com valor `data` = 10 (4 bytes), que é somado com o valor do tamanho de `next` (próximo elemento) que ocupa 8 bytes, então basicamente, nesse modelo de arquitetura desse código, uma posição da lista com `data` e `next` ocupam 12 bytes, e por último soma-se o valor de `head` que também ocupa 8 bytes neste exemplo. Resumindo, o cálculo fica: `tamanhoElemento*quantidadeDeElementos + tamanhoHead`. Se a lista tiver 1 elemento, ocupará 20 bytes, e se tiver 2 elementos, ocupará o total de 32 bytes na memória do computador.

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_LinkedLists_Exemplo1.png?raw=true)

Mesmo que o próximo elemento seja nulo,  `null` e `next` têm o mesmo tamanho.

**Função para remover e liberar a memória de um elemento da lista:**

```c
void removeElement(LinkedList* list, int value) {
    Node* current = list->head;
    Node* previous = NULL;

    // Procura o nó com o valor fornecido
    while (current != NULL && current->data != value) {
        previous = current;
        current = current->next;
    }

    if (current == NULL) {
        printf("Elemento %d não encontrado na lista.\n", value);
        return;
    }

    // Atualiza os ponteiros para remover o nó da lista
    if (previous == NULL) {
        list->head = current->next;  // Se o nó a ser removido é o primeiro
    } else {
        previous->next = current->next;
    }

    free(current);  // Libera a memória do nó removido
    list->size--;   // Decrementa o número de elementos na lista
}
```

**Função para liberar toda a memória da lista:**

```c
void freeList(LinkedList* list) {
    Node* current = list->head;
    Node* next;

    // Libera a memória de cada nó na lista
    while (current != NULL) {
        next = current->next;
        free(current);
        current = next;
    }

    free(list);  // Libera a memória da estrutura da lista
}
```

**Função principal:**

```c
int main() {
    // Cria uma lista vazia
    LinkedList* myList = createList();

    // Adiciona alguns elementos à lista
    append(myList, 1);
    append(myList, 2);

    // Imprime a lista inicial
    printf("Lista inicial:\n");
    printList(myList);

    // Remove um elemento da lista
    removeElement(myList, 20);
    printf("\nLista após remover o elemento 20:\n");
    printList(myList);

    // Libera toda a memória alocada para a lista
    freeList(myList);

    return 0;
}
```

**Código completo:**

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;            
    struct Node* next;   
} Node;

typedef struct {
    Node* head;   
    int size;     
} LinkedList;

LinkedList* createList() {
    LinkedList* list = (LinkedList*)malloc(sizeof(LinkedList));  
    if (list == NULL) {  
        perror("Erro ao alocar memória para a lista"); 
        exit(EXIT_FAILURE);  
    }
    list->head = NULL;
    list->size = 0;     
    return list;
}

void append(LinkedList* list, int value) {
    Node* newNode = (Node*)malloc(sizeof(Node)); 
    if (newNode == NULL) {  
        perror("Erro ao alocar memória para o novo nó");
        exit(EXIT_FAILURE); 
    }
    newNode->data = value;   
    newNode->next = NULL;    

    if (list->head == NULL) {
        list->head = newNode;  
    } else {
        Node* current = list->head;
        while (current->next != NULL) {
            current = current->next;  
        }
        current->next = newNode;  
    }

    list->size++;  
}

void printList(LinkedList* list) {
    Node* current = list->head;
   size_t totalSize = 0;
    while (current != NULL) {
        printf("%d (Tamanho: %zu bytes) -> ", current->data, sizeof(current->data));
      totalSize += sizeof(Node);
        current = current->next;
    }
    printf("NULL\n");

  printf("Tamanho total da lista: %zu bytes\n", totalSize);
}

void removeElement(LinkedList* list, int value) {
    Node* current = list->head;
    Node* previous = NULL;

    while (current != NULL && current->data != value) {
        previous = current;
        current = current->next;
    }

    if (current == NULL) {
        printf("Elemento %d não encontrado na lista.\n", value);
        return;
    }

    if (previous == NULL) {
        list->head = current->next; 
    } else {
        previous->next = current->next;
    }

    free(current); 
    list->size--;  
}

void freeList(LinkedList* list) {
    Node* current = list->head;
    Node* next;

    while (current != NULL) {
        next = current->next;
        free(current);
        current = next;
    }

    free(list); 
}

int main() {
    LinkedList* myList = createList();

    append(myList, 1);
    append(myList, 2);

    printf("Lista inicial:\n");
    printList(myList);

    removeElement(myList, 20);
    printf("\nLista após remover o elemento 20:\n");
    printList(myList);

    freeList(myList);

    return 0;
}
```

## Esclarecimentos

Esta lógica pode parecer complexa, mas por a linguagem C se tratar de uma linguagem de baixo nível, devemos utilizar essas estratégias para ter um bom uso do hardware do computador e evitar problemas de eficiência e desempenho do nosso programa. Em outras linguagens como o Java, que é considerado de alto nível, esse tipo de abordagem não é necessário durante o desenvolvimento dos nosso projetos, pois a JVM (Java Virtual Machine) já trata desses problemas automaticamente, não sendo necessário alocar ou desalocar memória manualmente, como por exemplo, ao criar um `ArrayList` em Java, já se trata de uma lista encadeada que adiciona elementos dinamicamente e a própria JVM cuida do gerenciamento de memória.
