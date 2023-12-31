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

## Lista ligada

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

## Lista duplamente ligada

A lista duplamente ligada funciona de forma parecida com o exemplo anterior, mas além de ter um ponteiro apontando para o próximo elemento, também contém um ponteiro que aponta para o anterior para navegação bidimensional dos elementos.

Exemplo:

```c
#include <stdio.h>
#include <stdlib.h>

// Estrutura do Nó (Node) para representar um elemento na lista duplamente
// ligada
typedef struct Node {
  int data;          // Valor do elemento
  struct Node *next; // Ponteiro para o próximo elemento na sequência
  struct Node *prev; // Ponteiro para o elemento anterior na sequência
} Node;

// Estrutura da Lista Duplamente Ligada
typedef struct {
  Node *head; // Ponteiro para o primeiro nó na lista
  Node *tail; // Ponteiro para o último nó na lista
  int size;   // Número de elementos na lista
} DoublyLinkedList;

// Função para criar um novo nó
Node *createNode(int data) {
  Node *newNode = (Node *)malloc(sizeof(Node));
  if (newNode == NULL) {
    perror("Erro ao alocar memória para o novo nó");
    exit(EXIT_FAILURE);
  }

  newNode->data = data;
  newNode->next = NULL;
  newNode->prev = NULL;

  return newNode;
}

// Função para adicionar um elemento no final da lista duplamente ligada
void append(DoublyLinkedList *list, int data) {
  Node *newNode = createNode(data);

  if (list->head == NULL) {
    // Se a lista está vazia, o novo nó é o primeiro e o último
    list->head = newNode;
    list->tail = newNode;
  } else {
    // Adiciona o novo nó ao final da lista
    list->tail->next = newNode;
    newNode->prev = list->tail;
    list->tail = newNode;
  }

  list->size++;
}

// Função para adicionar um elemento no início da lista duplamente ligada
void prepend(DoublyLinkedList *list, int data) {
  Node *newNode = createNode(data);

  if (list->head == NULL) {
    // Se a lista está vazia, o novo nó é o primeiro e o último
    list->head = newNode;
    list->tail = newNode;
  } else {
    // Adiciona o novo nó no início da lista
    newNode->next = list->head;
    list->head->prev = newNode;
    list->head = newNode;
  }

  list->size++;
}

void insertAt(DoublyLinkedList *list, int data, int position) {
  if (position < 0 || position > list->size) {
    printf("Posição inválida. A lista possui %d elementos.\n", list->size);
    return;
  }

  // Cria o novo nó
  Node *newNode = createNode(data);

  // Caso especial: inserção no início
  if (position == 0) {
    prepend(list, data);
    return;
  }

  // Caso especial: inserção no final
  if (position == list->size) {
    append(list, data);
    return;
  }

  // Percorre a lista até a posição desejada
  Node *current = list->head;
  for (int i = 0; i < position - 1; i++) {
    current = current->next;
  }

  // Atualiza os ponteiros do novo nó
  newNode->next = current->next;
  newNode->prev = current;

  // Atualiza os ponteiros dos nós ao redor do novo nó
  current->next->prev = newNode;
  current->next = newNode;

  list->size++;
}

// Função para imprimir a lista duplamente ligada
void printList(DoublyLinkedList *list) {
  Node *current = list->head;

  printf("Lista Duplamente Ligada:\n");
  while (current != NULL) {
    printf("%d -> ", current->data);
    current = current->next;
  }
  printf("NULL\n");
}

int main() {
  DoublyLinkedList myList = {NULL, NULL, 0};

  // Adiciona alguns elementos à lista (ao final)
  append(&myList, 10);
  append(&myList, 20);
  append(&myList, 30);

  // Imprime a lista
  printList(&myList);

  // Adiciona um elemento no início da lista
  prepend(&myList, 5);
  
  // Insere um elemento na posição 2
  insertAt(&myList, 15, 2);

  // Imprime a lista novamente
  printList(&myList);

  return 0;
}
```

As principais diferenças é que além do rastreio do elemento anterior, também podemos inserir no meio da lista atualizando tanto o anterior quanto o próximo na mesma operação.

**Função adicionar ao começo:**

```c
void prepend(DoublyLinkedList *list, int data) {
  Node *newNode = createNode(data);

  if (list->head == NULL) {
    // Se a lista está vazia, o novo nó é o primeiro e o último
    list->head = newNode;
    list->tail = newNode;
  } else {
    // Adiciona o novo nó no início da lista
    newNode->next = list->head;
    list->head->prev = newNode;
    list->head = newNode;
  }

  list->size++;
}
```

Aqui adicionamos ao início da lista, verificando se a lista já contém elementos, do contrário ele é o primeiro da lista e último ao mesmo tempo, se não, pegamos o anterior e adicionamos nosso novo valor.

**Função adicionar ao meio da lista:**

```c
void insertAt(DoublyLinkedList *list, int data, int position) {
  if (position < 0 || position > list->size) {
    printf("Posição inválida. A lista possui %d elementos.\n", list->size);
    return;
  }

  // Cria o novo nó
  Node *newNode = createNode(data);

  // Caso especial: inserção no início
  if (position == 0) {
    prepend(list, data);
    return;
  }

  // Caso especial: inserção no final
  if (position == list->size) {
    append(list, data);
    return;
  }

  // Percorre a lista até a posição desejada
  Node *current = list->head;
  for (int i = 0; i < position - 1; i++) {
    current = current->next;
  }

  // Atualiza os ponteiros do novo nó
  newNode->next = current->next;
  newNode->prev = current;

  // Atualiza os ponteiros dos nós ao redor do novo nó
  current->next->prev = newNode;
  current->next = newNode;

  list->size++;
}
```

Primeiro criamos o nó desejado e usamos as outras funções já criadas caso a posição seja a primeira ou a última da lista, demais valores de posição atualizam os ponteiros tanto do atual, como também do anterior e do próximo de maneira que ambos continuem apontando um para o outro sem quebrar a lista.

Resultado:

![Example2](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_LinkedLists_Exemplo2.png?raw=true)


## Exemplos de contexto de uso:

### Em que as listas ligadas são utilizadas?

- **Gerenciamento de Memória Dinâmica:** Listas ligadas são amplamente utilizadas em linguagens de programação para alocar e desalocar memória dinamicamente. Elas oferecem flexibilidade ao acomodar dados de tamanhos variáveis durante a execução do programa.

- **Implementação de Estruturas de Dados Avançadas:** Listas ligadas são a base para outras estruturas de dados, como pilhas, filas, e árvores. Elas facilitam a construção de estruturas dinâmicas que podem ser adaptadas conforme necessário.

### Em que as listas duplamente ligadas são utilizadas?

- **Implementação de Editores de Texto e Documentos:** Em editores de texto, as listas duplamente ligadas podem ser usadas para representar o conteúdo do documento, permitindo operações eficientes de inserção e remoção de texto em qualquer ponto do documento.
