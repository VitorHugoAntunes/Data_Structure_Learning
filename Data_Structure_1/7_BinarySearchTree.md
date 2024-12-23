# 7 - Árvores Binárias de Busca (BST)

Entenda árvores binárias de busca e suas propriedades.

A lógica da árvore binária de busca (BST) funciona de forma parecida com uma árvore binária comum, mas consiste em adicionar ao lado esquerdo os valores que são menores que o conteúdo do nó e ao lado direito os valores que são maiores. Isso cria uma estrutura hierárquica onde cada nó pode ser considerado uma folha se não tiver filhos, ou seja, se ambos os nós à esquerda e à direita forem nulos. O exemplo de código em C a seguir demonstra a implementação dessa estrutura, utilizando structs para representar cada nó da árvore, contendo referências para seus possíveis filhos, e uma struct para representar a própria árvore, que inclui a raiz como o primeiro elemento da hierarquia.

Esta técnica é muito interessante para busca, pois se o valor que desejamos encontrar é menor ou maior que a raiz, eliminamos metade dos elementos da árvore durante o processo e tornamos a busca muito mais rápida e eficiente.

```c
#include <stdio.h>

// Definição da estrutura do nó da árvore binária
typedef struct no {
  int conteudo;
  struct no *esquerda, *direita;
} No;

// Definição da estrutura da árvore binária
typedef struct {
  No *raiz;
} ArvoreBinaria;

// Necessário adicionar protótipos das funções para evitar erros de compilação por chamadas cruzadas
void inserirEsquerda(No *no, int valor);
void inserirDireita(No *no, int valor);

// Função para inserir um valor na subárvore esquerda de um nó
void inserirEsquerda(No *no, int valor) {
  if (no->esquerda == NULL) {
    // Cria um novo nó e o adiciona à subárvore esquerda
    No *novo = (No *)malloc(sizeof(No));
    novo->conteudo = valor;
    novo->esquerda = NULL;
    novo->direita = NULL;
    no->esquerda = novo;
  } else {
    // Se o valor for menor, insere na subárvore esquerda; se for maior, na subárvore direita
    if (valor < no->esquerda->conteudo)
      inserirEsquerda(no->esquerda, valor);
    if (valor > no->esquerda->conteudo)
      inserirDireita(no->esquerda, valor);
  }
}

// Função para inserir um valor na subárvore direita de um nó
void inserirDireita(No *no, int valor) {
  if (no->direita == NULL) {
    // Cria um novo nó e o adiciona à subárvore direita
    No *novo = (No *)malloc(sizeof(No));
    novo->conteudo = valor;
    novo->esquerda = NULL;
    novo->direita = NULL;
    no->direita = novo;
  } else {
    // Se o valor for maior, insere na subárvore direita; se for menor, na subárvore esquerda
    if (valor > no->direita->conteudo)
      inserirDireita(no->direita, valor);
    if (valor < no->direita->conteudo)
      inserirEsquerda(no->direita, valor);
  }
}

// Função para imprimir a árvore de forma organizada
void imprimir(No *raiz, int espacamento) {
  if (raiz == NULL)
    return;

  // Aumenta o espaço entre os níveis
  espacamento += 5;
  int i;

  // Imprime o nó da direita
  imprimir(raiz->direita, espacamento);

  // Imprime este nó com um espaçamento adequado
  printf("\n");
  for (i = 5; i < espacamento; i++)
    printf(" ");
  printf("%d\n", raiz->conteudo);

  // Imprime o nó da esquerda
  imprimir(raiz->esquerda, espacamento);
}

// Função para inserir um valor na árvore
void inserir(ArvoreBinaria *arv, int valor) {
  if (arv->raiz == NULL) {
    // Se a árvore estiver vazia, cria um novo nó e o torna a raiz da árvore
    No *novo = (No *)malloc(sizeof(No));
    novo->conteudo = valor;
    novo->esquerda = NULL;
    novo->direita = NULL;
    arv->raiz = novo;
  } else {
    // Se a árvore não estiver vazia, chama as funções de inserção esquerda ou direita
    if (valor < arv->raiz->conteudo)
      inserirEsquerda(arv->raiz, valor);
    if (valor > arv->raiz->conteudo)
      inserirDireita(arv->raiz, valor);
  }
}

// Função principal
int main() {
  int op, valor;
  ArvoreBinaria arv;
  arv.raiz = NULL;

  do {
    // Menu de opções
    printf("\n0 - Sair\n1 - Inserir\n2 - Imprimir\n");
    scanf("%d", &op);

    switch (op) {
    case 0:
      printf("\nSaindo...\n");
      break;
    case 1:
      // Solicita um valor e insere na árvore
      printf("Digite um valor: ");
      scanf("%d", &valor);
      inserir(&arv, valor);
      break;
    case 2:
      // Imprime a árvore de forma organizada
      printf("\nImpressao da arvore binaria:\n");
      imprimir(arv.raiz, 0);
      break;
    default:
      printf("Opção inválida!\n");
    }
  } while (op != 0);

  return 0;
}
```

Resultado após inserir alguns valores manualmente pelo menu:

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_BinarySearchTree_Exemplo1.png?raw=true)

**Função para contar quantos elementos tem na árvore:**

```c
int tamanho(No *raiz) {
  if (raiz == NULL) {
    return 0;
  } else {
    return 1 + tamanho(raiz->esquerda) + tamanho(raiz->direita);
  }
}
```

**Função para buscar um elemento na árvore:**

```c
int buscarElemento(No *raiz, int chave) {
  if (raiz == NULL) {
    return -1;
  } else {
    if (raiz->conteudo == chave) {
      return raiz->conteudo;
    } else {
      if (chave < raiz->conteudo) {
        return buscarElemento(raiz->esquerda, chave);
      } else {
        return buscarElemento(raiz->direita, chave);
      }
    }
  }
}
```

**Nova função `main` que agrega essas funções adicionadas:**

```c
int main() {
  int op, valor;
  ArvoreBinaria arv;
  arv.raiz = NULL;

  do {
    printf("\n0 - Sair\n1 - Inserir\n2 - Imprimir\n3 - Buscar\n");
    scanf("%d", &op);

    switch (op) {
    case 0:
      printf("\nSaindo...\n");
      break;
    case 1:
      printf("Digite um valor: ");
      scanf("%d", &valor);
      inserir(&arv, valor);
      break;
    case 2:
      printf("\nImpressao da arvore binaria:\n");
      imprimir(arv.raiz, 0);
      printf("\nQuantidade de elementos desta arvore binaria: %d",
             tamanho(arv.raiz));
      break;
    case 3:
      printf("Digite um valor para buscar na arvore binaria: ");
      scanf("%d", &valor);
      printf("Valor encontrado: %d", buscarElemento(arv.raiz, valor));
    default:
      printf("Opção inválida!\n");
    }
  } while (op != 0);
}
```

### Mas como funcionaria a remoção de um elemento da árvore binária?

A lógica para remover um elemento necessita ficar atento em 3 detalhes importantes:

- Remover um nó folha (nó sem filhos);
- Remover um nó que contém apenas um filho;
- Remover um nó que contém dois filhos.

Segue abaixo bloco de código com esta lógica. As explicações do fluxo estão como comentários no código:

```c
// Função para buscar o menor valor na subárvore direita
No *obterSucessor(No *atual) {
  atual = atual->direita;
  while (atual != NULL && atual->esquerda != NULL)
    atual = atual->esquerda;
  return atual;
}

No *remover(No *raiz, int chave) {

  // Se a raiz for vazia
  if (raiz == NULL)
    return raiz;

  // Busca a chave na subárvore corretamente
  if (raiz->conteudo > chave)
    raiz->esquerda = remover(raiz->esquerda, chave); // Procura na subárvore esquerda
  else if (raiz->conteudo < chave)
    raiz->direita = remover(raiz->direita, chave); // Procura na subárvore direita
  else {
    // Encontrou o nó com a chave a ser removida

    // Caso 1: o nó não tem filhos ou tem apenas o filho direito
    if (raiz->esquerda == NULL) {
      No *temp = raiz->direita;
      free(raiz);
      return temp;
    }

    // Caso 2: o nó tem apenas o filho esquerdo
    if (raiz->direita == NULL) {
      No *temp = raiz->esquerda; // Armazena o filho direito
      free(raiz); // Libera a memória do nó atual
      return temp; // Retorna o filho direito (pode ser NULL)
    }

    // Caso 3: o nó tem ambos os filhos
    No *sucessor = obterSucessor(raiz);
    raiz->conteudo = sucessor->conteudo;
    raiz->direita = remover(raiz->direita, sucessor->conteudo);
  }
  return raiz;
}

// dentro da função main adicionar ao menu:

// Menu de opções
  printf("\n0 - Sair\n1 - Inserir\n2 - Imprimir\n3 - Buscar\n4 - Remover\n5 - Tamanho\n");

//...
case 4:
  printf("Digite um valor a ser removido: ");
  scanf("%d", &valor);
  arv.raiz = remover(arv.raiz, valor);
  break;
//...
```

Resultado:

![Example2](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_BinarySearchTree_Exemplo2.png?raw=true)

Nesta implementação, se um nó a ser removido tem dois filhos, encontra-se o menor nó na subárvore direita que não possui filho esquerdo (sucessor in-order) e troca-se o valor entre esse nó e o nó a ser removido. Em seguida, realiza-se uma chamada recursiva para remover o sucessor na subárvore direita.

Essa abordagem é conhecida como substituição pelo sucessor in-order e é uma maneira eficiente de manter a ordem na árvore binária durante a remoção.

Há outras maneiras mais eficientes, como a exclusão por fusão, que se resume em remover o nó a ser excluído e depois funde as subárvores esquerda e direita desse nó em uma única subárvore.

Apesar do código acima parecer verboso, é uma maneira mais didática de como entender o fluxo de manipulação de ponteiros dentro de uma árvore binária.

Também há outros tipos de estratégias, como a remoção em cascata, que remove os filhos do nó excluído sucessivamente, como funciona quando você apaga um diretório que contém arquivos dentro.



## Exemplos de contexto de uso:

### No que as árvores binárias de busca são utilizadas?

1. **Mapas e Conjuntos Eficientes:**
    - Implementações de mapas e conjuntos frequentemente usam BSTs para fornecer operações eficientes de busca, inserção e remoção de elementos.
2. **Dicionários e Corretores Ortográficos:**
    - Em dicionários e corretores ortográficos, são empregadas para armazenar e recuperar rapidamente palavras, proporcionando uma busca eficiente em ordem alfabética.
3. **Agendamento de Eventos:**
    - Em sistemas de tempo real, como sistemas operacionais de tempo real ou jogos, podem ser usadas para agendar eventos em ordem de tempo, facilitando a execução de tarefas em momentos específicos.
