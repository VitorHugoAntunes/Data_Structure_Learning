# 8 - Heap

Aprenda sobre heaps (binários, binomiais, Fibonacci) e suas operações (inserir, extrair ou remover mínimo/máximo).

## Definição

Um heap é uma árvore binária especializada que satisfaz a propriedade de heap. A propriedade de heap é uma propriedade de ordem que diz que cada nó é maior (ou menor) que seus filhos, dependendo se é um heap máximo ou mínimo.

Abaixo temos um bloco de código em C que cria um heap binário máximo. Basicamente, criamos um array para a heap e funções para inserir um novo elemento, obter o máximo, obter o mínimo, remover o máximo e imprimir a heap.

```c
#include <stdio.h>
#include <stdlib.h>

#define TAMANHO_MAXIMO 7

int pai(int i) {
  return (i - 1) / 2; // retorna o índice do pai do nó i, no caso, a raiz
}

int esquerda(int i) {
  return 2 * i + 1; // retorna o índice do filho esquerdo do nó i
}

int direita(int i) {
  return 2 * i + 2; // retorna o índice do filho direito do nó i
}

// Função para trocar dois elementos de posição
void trocar(int *a, int *b){
  int temp = *a;
  *a = *b;
  *b = temp;
}

// Função para inserir um novo elemento na heap
void inserir(int a[], int novo, int *n){ // *n é o últomo elemento da heap, logo, é o tail
  if (*n >= TAMANHO_MAXIMO){
    printf("Heap cheia!\n");
    return;
  }

  a[*n] = novo;
  *n = *n + 1;

  int i = *n - 1; // Índice do novo elemento
  
  // Reorganiza a heap para manter a propriedade de heap
  while (i > 0 && a[pai(i)] < a[i]){
    trocar(&a[i], &a[pai(i)]);
    i = pai(i);
  }
}

// Função max heapify, que reorganiza a heap para manter a propriedade de heap
void reordenarParaHeapMaximo(int a[], int i, int n){
  int maior = i;

  int esq = esquerda(i);
  int dir = direita(i);

  if (esq < n && a[esq] > a[maior]){
    maior = esq;
  }

  if (dir < n && a[dir] > a[maior]){
    maior = dir;  
  }

  if (maior != i){
    int temp = a[i];
    a[i] = a[maior];
    a[maior] = temp;
    reordenarParaHeapMaximo(a, maior, n);
  }
}

int obterMaximo(int a[], int *n){
  printf("Valor na raiz: %d\n", a[0]);
  return a[0];
}

int obterMinimo(int a[], int *n){
  printf("Ultimo valor no heap: %d\n", a[*n-1]);
  return a[*n-1];
}

int removerMaximo(int a[], int *n){
  int maximo = a[0];
  a[0] = a[*n-1];
  *n = *n - 1;

  reordenarParaHeapMaximo(a, 0, *n);
  return maximo;
}

void imprimirHeap(int a[], int n){
  for (int i = 0; i < n; i++){
    printf("Posição %d: %d\n", i, a[i]);
    printf("\n");
  }
}
```

Dada a estrutura {10, 5, 71, 43, 21, 2, 18} e seguindo a fórmula de cálculo de índices de filhos e pai demonstrada no código acima, temos a seguinte representação de um heap binário máximo:

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_Heap_Exemplo1.png?raw=true)

Agora, vamos adicionar a função main para testar as funções de heap:

```c
// Função principal
int main() {
  int n = 0;
  int a[TAMANHO_MAXIMO];

  inserir(a, 10, &n);
  inserir(a, 5, &n);
  inserir(a, 71, &n);
  inserir(a, 43, &n);
  inserir(a, 21, &n);
  inserir(a, 2, &n);
  inserir(a, 18, &n);

  imprimirHeap(a, n);

  obterMaximo(a, &n);

  obterMinimo(a, &n);

  return 0;
}
```

A saída do código acima será:

![Example2](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_Heap_Exemplo2.PNG?raw=true)

Veja que o resultado bate com a representação do heap binário máximo que fizemos anteriormente.
Abaixo, temos uma nova representação do heap binário máximo após a remoção do máximo, logo, o nó 71 deve ser removido e o nó 43 deve ser promovido para a raiz:

![Example3](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_Heap_Exemplo3.PNG?raw=true)

Agora, vamos adicionar a função de remoção de máximo na função ```main``` e reimprimir a heap:

```c
  removerMaximo(a, &n);
  imprimirHeap(a, n);
```

A saída do código acima será:

![Example4](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_Heap_Exemplo4.PNG?raw=true)

Veja que o resultado bate com a nova representação do heap binário máximo que fizemos anteriormente.

## Exemplos de contexto de uso:

### No que heaps binários são utilizados?

1. **Ordenação eficiente:** 
    - Heaps binários são utilizados para ordenar elementos de forma eficiente. A complexidade de tempo para ordenar n elementos é O(n log n).

2. **Implementação de filas de prioridade:**
    - Heaps binários são utilizados para implementar filas de prioridade. O elemento com maior prioridade é sempre o primeiro a ser removido.

3. **Algoritmos de grafos:**
    - Heaps binários são utilizados em algoritmos de grafos como Dijkstra e Prim para encontrar o caminho mais curto e a árvore geradora mínima, respectivamente.