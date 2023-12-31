# 6 - Recursividade

Compreenda a recursividade, que é fundamental para muitas estruturas e algoritmos.

## Definição

A recursividade é um conceito em programação e matemática em que uma função se chama a si mesma durante sua execução. Uma função recursiva não usa um loop para repetir uma determinada operação, mas chama a si mesma para realizar a tarefa em partes menores.

Exemplo:

O fatorial de 5 é 5 * 4 * 3 * 2 * 1.

O fatorial de 4 é 4 * 3 * 2 * 1.

O fatorial de 3 é 3 * 2 * 1.

O fatorial de 2 é 2 * 1.

O fatorial de 1 é 1.

Basicamente, o fatorial de 5 é 5! = 5 * 4!.

Definição recursiva deste algoritmo é **N! = N * (N-1)!.**

Cada recursão necessita um ponto de parada para não gerar um loop infinito no algoritmo e é chamado de base da recursão; consiste na versão mais simples possível do problema.

Para o problema do fatorial, a base é o fatorial de 0, que é definido como valendo 1.

Exemplo da implementação em C:

```c
int fatorial (int N) { 
     if(N==0) return 1;  // Esta é a base da recursao
     else return N * fatorial (N-1); // A chamada recursiva
}

int main() {
  int n;
  
  printf("Digite um valor inteiro para calcular o fatorial: ");
  scanf("%d", &n);

  printf("Resulatado do fatorial de %d: %d", n, fatorial(n));
}
```

Resultado:

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_Recursion_Exemplo1.png?raw=true)

## Exemplos de contexto de uso:

### Como a Recursividade é Utilizada?

1. **Problemas Matemáticos Recursivos:**
    - A recursividade é aplicada em soluções para problemas matemáticos complexos que podem ser divididos em subproblemas menores. Um exemplo é a sequência de Fibonacci, onde F(n)=F(n−1)+F(n−2) e a função é chamada recursivamente para n−1 e n−2.
2. **Solução de Problemas de Combinatória:**
    - Usada para resolver problemas de combinatória, como a geração de todas as combinações ou permutações de um conjunto.
3. **Análise de Estruturas de Dados Recursivas:**
    - Como listas encadeadas ou árvores, a recursividade é naturalmente incorporada para manipular cada nível da estrutura.
4. **Implementação de Algoritmos Dividir e Conquistar:**
    - Frequentemente utilizam recursividade como o mergesort, quicksort e o algoritmo de busca binária.
5. **Navegação em Estruturas de Diretório:**
    - Pode ser empregada para navegar em estruturas de diretório, visitando todos os arquivos e subdiretórios de maneira eficiente.
