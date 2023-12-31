# 3 - Filas e pilhas

Compreenda as filas (queues) e pilhas (stacks) e suas operações (enqueue, dequeue, push, pop).

## Fila

Uma fila (em inglês, queue) é uma estrutura de dados que segue a lógica do "primeiro a entrar, primeiro a sair" (FIFO - First-In-First-Out). É semelhante a uma fila na vida real, onde a pessoa que chega primeiro é a primeira a ser atendida.

Os elementos em uma fila são organizados em uma ordem linear. Quando um novo elemento é adicionado à fila, ele é colocado no final da fila. Quando um elemento é removido da fila, é retirado do início da fila.

A seguir temos um exemplo de funcionamento de uma fila:

```c
#include <stdio.h>
#include <stdlib.h>

#define Elementos_Fila 4

// Estrutura da fila
typedef struct {
  int vetor[Elementos_Fila];
  int fim;
} Fila;

// Adiciona ao final da fila
int incluiElemento(Fila *f, int n) {
  if(f->fim >= Elementos_Fila) {
    printf("\nFila cheia. Não é possível adicionar mais elementos.");
  } else {
    f->vetor[f->fim] = n;
    f->fim++;
  }

  return 0;
}

// Retira do inicio da fila
int deslocaFila(Fila *f, int n) {
  if (n > f->fim) {
    printf(
        "\n\nNão é possível remover mais elementos do que a fila suporta.\n");
  } else {
    for (int i = 0; i < f->fim - n; i++) {
      f->vetor[i] = f->vetor[i + n];
    }
    f->fim -= n;
  }

  return 0;
}

// Verifica se a fila está vazia e retorna seus valores de cada index
int retornaFila(Fila *f) {
  if (f->fim != 0) {
    for (int i = 0; i < f->fim; i++) {
      printf("%d ", f->vetor[i]);
    }

  } else {
    printf("Nenhum elemento. A fila está vazia.");
  }

  printf("\nTamanho atual da fila: %d\n", f->fim);
  return 0;
}

int main(void) {
  Fila f;
  f.fim = 0;

  // Passando a referência do ponteiro da fila na memória
  printf("Fila inicial: \n");
  retornaFila(&f);

	// Adicionando manualmente os elementos na fila
  incluiElemento(&f, 5);
  incluiElemento(&f, 3);
  incluiElemento(&f, 4);
  incluiElemento(&f, 9);
  incluiElemento(&f, 9);

  printf("\n\nFila depois do enqueue (enfileiramento): \n");
  retornaFila(&f);

	// Definindo quantos elementos serão removidos do início da fila
  deslocaFila(&f, 2);

  printf("\n\nFila depois do dequeue (desenfileiramento ou deslocamento): \n");
  retornaFila(&f);
}
```

Resultado:

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_QueuesAndStacks_Exemplo1.png?raw=true)

O mesmo exemplo em Java:

```java
public class Fila {
    private int[] vetor;
    private int fim;

    // Construtor para inicializar a fila
    public Fila(int tamanho) {
        this.vetor = new int[tamanho];
        this.fim = 0;
    }
    public void incluiElemento(int n) {
        if (fim < vetor.length) {
            vetor[fim] = n;
            fim++;
        } else {
            System.out.println("Fila cheia. Não é possível adicionar mais elementos.");
        }
    }

    public void deslocaFila(int n) {
        if(n > fim){
            System.out.println("Não é possível remover mais elementos do que a fila suporta.");
        } else {
            for (int i = 0; i < fim - n; i++) {
                vetor[i] = vetor[i + n];
            }

            fim -= n;
        }
    }

    public void imprimeFila() {
        if(fim != 0){
            System.out.print("Fila: ");
            for (int i = 0; i < fim; i++) {
                System.out.print(vetor[i] + " ");
            }
            System.out.println();
        } else {
            System.out.println("Nenhum elemento. A fila está vazia.");
        }

        System.out.println("Tamanho atual da fila: " + fim);
    }
}

public class Main {
    public static void main(String[] args) {
        // Cria uma instância da classe Fila
        Fila fila = new Fila(4);

        System.out.println("Fila inicial:");
        fila.imprimeFila();

        // Usa a instância para chamar os métodos não estáticos
        fila.incluiElemento(5);
        fila.incluiElemento(3);
        fila.incluiElemento(4);
        fila.incluiElemento(9);

        System.out.println("Fila depois do enqueue (enfileiramento): ");
        fila.imprimeFila();

        fila.deslocaFila(2);

        System.out.println("Fila depois do dequeue (desenfileiramento ou deslocamento):");
        fila.imprimeFila();
    }
}
```

## Pilha

Uma pilha (em inglês, stack) é uma estrutura de dados que segue a lógica do "último a entrar, primeiro a sair" (LIFO - Last-In-First-Out). Um exemplo real pode ser uma pilha de livros, que não é possível remover o primeiro (mais abaixo) da pilha, necessário tirar o que está ao topo, que consequentemente foi o último a entrar.

A pilha trabalha com duas operações principais:

- Empilhar:
    - Adiciona um novo elemento ao topo e incrementa-o;
    - Gera stack overflow (pilha cheia) se topo = n;
- Desempilhar:
    - Remove um elemento do topo e decrementa-o;
    - Gera stack empty (pilha vazia) se topo = 0;
    

Exemplo em C:

```c
#include <stdio.h>
#include <stdlib.h>

#define TAMANHO_PILHA 20

typedef struct {
  int vetor[TAMANHO_PILHA];
  int topo;
} Pilha;

int incluiElemento(Pilha *p, int n) {
  if (p->topo >= TAMANHO_PILHA) {
    printf("\nPilha cheia. Não é possível adicionar mais elementos.");
  } else {
    p->vetor[p->topo] = n;
    p->topo++;
  }

  return 0;
}

int removeElemento(Pilha *p) {
  if(p->topo == 0){
    printf( "\nPilha vazia. Não é possível remover elementos.");
  } else {
    p->topo--;
  }

  return 0;
}

int retornaPilha(Pilha *p) {
  if (p->topo != 0) {
    for (int i = 0; i < p->topo; i++) {
      printf("%d ", p->vetor[i]);
    }

  } else {
    printf("Nenhum elemento. A Pilha está vazia.");
  }

  printf("\nTamanho atual da pilha: %d\n", p->topo);
  return 0;
}

int main(void) {
  Pilha p;
  p.topo = 0;

  printf("Pilha inicial: \n");
  retornaPilha(&p);

  incluiElemento(&p, 5);
  incluiElemento(&p, 3);
  incluiElemento(&p, 4);
  incluiElemento(&p, 4);

  printf("\n\nPilha depois do push (adicionar ao topo): \n");
  retornaPilha(&p);

  removeElemento(&p);

  printf("\n\nPilha depois do pop (remover o ultimo): \n");
  retornaPilha(&p);
}
```

Resultado:

![Example2](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_QueuesAndStacks_Exemplo2.png?raw=true)

## Exemplos de contexto de uso:

### No que as filas são utilizadas?

- Sistemas de Gerenciamento de Tarefas: Filas são frequentemente usadas em sistemas operacionais para gerenciar tarefas e processos. As tarefas são colocadas em uma fila de execução e processadas na ordem em que foram recebidas.
- Impressão e Processamento em Lote: As filas são úteis para gerenciar trabalhos de impressão, onde os documentos a serem impressos são processados na ordem de chegada.

### No que as pilhas são utilizadas?

- `Undo/Redo` em Aplicações: Pilhas são usadas para implementar operações "Desfazer" e "Refazer" em aplicativos, permitindo aos usuários reverter ações utilizando o `ctrl-z`.
- Chamadas de Funções e Recursão: Pilhas são utilizadas para gerenciar chamadas de funções e a execução de operações recursivas em linguagens de programação. Cada chamada de função é empilhada, e a execução retorna à função anterior quando a chamada é removida da pilha.
