# 5 - Árvores

Introdução às árvores binárias, suas propriedades e operações.

## Definição

A estrutura de dados em árvore é uma das mais importantes estruturas de dados não lineares utilizadas na programação. Diferentemente das listas e filas, nas quais os dados se encontram em sequência, nas árvores existe uma hierarquia na sua disposição.

As estruturas hierárquicas, conhecidas como árvores, contêm um conjunto finito de um ou mais elementos (nós), sendo um desses chamado de nó raiz
(ponto de entrada da estrutura). Cada nó pode possuir a associação de zero ou mais subconjuntos de nós, os quais são uma árvore denominada sub-árvore.

O nome "binária" é derivado do fato de que cada nó em uma árvore binária pode ter no máximo dois filhos.

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_BinaryTree_Exemplo1.png?raw=true)

Abaixo temos um bloco de código em C que cria uma estrutura de uma árvore binária. Basicamente, criamos um struct para a árvore contendo a raíz (primeiro elemento da hierarquia) e um struct para cada nó (elemento da árvore) que contém seu valor e um novo nó para esquerda e direita que conterá seus filhos. O nó pode ser chamado de folha caso não tenha filhos.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct no {
  int conteudo;
  struct no *esquerda, *direita;
} No;

// Função para criar um novo nó
No* criarNo(int valor) {
  No* novo = (No *)malloc(sizeof(No));
  novo->conteudo = valor;
  novo->esquerda = NULL;
  novo->direita = NULL;
  return novo;
}

// Função para inserir um valor na árvore
No* inserir(No* raiz, int valor) {
  if (raiz == NULL) {
    return criarNo(valor);
  }

  // Inserir aleatoriamente à esquerda ou à direita
  if (rand() % 2 == 0) {
    raiz->esquerda = inserir(raiz->esquerda, valor);
  } else {
    raiz->direita = inserir(raiz->direita, valor);
  }

  return raiz;
}

// Função para imprimir a árvore
void imprimir(No *raiz, int espacamento) {
  if (raiz == NULL)
    return;

  // Aumenta o espaço entre os níveis
  espacamento += 5;
  int i;

  // Imprime o nó da direita
  imprimir(raiz->direita, espacamento);

  // Imprime este nó
  printf("\n");
  for (i = 5; i < espacamento; i++)
    printf(" ");
  printf("%d\n", raiz->conteudo);

  // Imprime o nó da esquerda
  imprimir(raiz->esquerda, espacamento);
}

int main() {
  No* raiz = NULL;

  // Inserindo valores aleatoriamente na árvore
  raiz = inserir(raiz, 10);
  raiz = inserir(raiz, 5);
  raiz = inserir(raiz, 15);
  raiz = inserir(raiz, 3);
  raiz = inserir(raiz, 7);
  raiz = inserir(raiz, 12);
  raiz = inserir(raiz, 18);

  // Imprimindo a árvore em ordem
  printf("Árvore em ordem: ");
  imprimir(raiz, 0);
  printf("\n");

  return 0;
}
```

Esta lógica está usando números aleatórios para determinar qual lado o novo valor será inserido para balancear um pouco a árvore e não ter elementos apenas de um mesmo lado.

Resultado:

![Example2](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_BinaryTree_Exemplo2.png?raw=true)

Esta implementação usa como estratégia um recurso importante chamando recursividade, quando uma função ou código invoca ele mesmo dentro de sua execução formando um loop para se aprofundar na estrutura até o ponto de pausa (geralmente o final), que neste exemplo é quando não se tem mais nós.

**Veremos mais sobre recursividade no capítulo seguinte.**

## Exemplos de contexto de uso:

### No que as árvores binárias são utilizadas?

1. **Expressões Aritméticas e Árvores de Análise Sintática:**
    - Árvores binárias são usadas para representar a estrutura sintática de expressões matemáticas, facilitando a avaliação e a manipulação dessas expressões em compiladores e interpretadores.
2. **Árvores de Decisão:**
    - Em algoritmos de aprendizado de máquina, árvores binárias são utilizadas como estruturas para tomada de decisões hierárquicas em conjuntos de dados, especialmente em problemas de classificação.
3. **Sistemas de Arquivos:**
    - Alguns sistemas de arquivos utilizam árvores binárias para organizar e indexar os dados de maneira eficiente, facilitando operações como busca e recuperação de arquivos.
