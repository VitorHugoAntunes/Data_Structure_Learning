# 2 - Array e Listas

Aprenda sobre `arrays` e listas, estruturas que armazenam elementos de forma sequencial.

### Definição

`Array` é uma estrutura de dados que tem tamanho e tipo definidos que armazenam uma sequência de elementos.

Exemplo:

```java
int[] vetor = new int[5]; // tamanho de vetor 5
```

Diferente do C, em Java um `array` **não é uma estrutura primitiva**, mas sim um objeto que herda da classe `Object`.

É possível definir um `array` sem atribuir seus valores de cada posição no início, e cada posição será identificado com 0. Porém também pode criar uma lista de inicialização no momento da declaração do `array`:

```java
int[] vetor = {10, 15, 20, 35, 15}; // Lista de inicializacao
```

A notação acima pode ser usada tanto no tipo quanto no identificador da variável: `int[]` ou `vetor[]`.

Por razões de segurança, em Java não se pode acessar ou atribuir valores de uma posição da memória que não foi previamente criada para o `array`, ou seja, se tentar acessar a posição 6 de um `array` com 5 posições, será lançado uma `Exception error` na thread no seu programa. Diferente do C que permite o programa acessar parte da memória que não faz parte do seu vetor.

Em Java:

![Example1](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo1.png?raw=true)

Em C:

![Example2](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo2.png?raw=true)

### Outras formas de definir um `array` em Java:

Em Java também podemos inicializar um `array` a partir de uma classe invólucro:

```java
ArrayList<Integer> vetor3 = new ArrayList<>();
```

Aqui definimos um `array` de inteiros que por padrão de inicia vazio. Abaixo temos um exemplo de população dos seus valores, lembrando que desta forma não é um `array` convencional, mas sim um objeto de `array` que pode ser manipulado:

```java
ArrayList<Integer> vetor3 = new ArrayList<>();

for (int i=0; i<5; i++) {
	vetor3.add(i * 10);
}

System.out.println(vetor3);
```

`ArrayList` é uma implementação de `List` que vem de uma biblioteca importada do Java, e tem capacidade dinâmica, por isso não informamos o tamanho.

Retorna:

![Example3](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo3.png?raw=true)

Exemplo em C:

```c
int vetor1[5];
int vetor2[5] = {10, 15, 20, 35, 15}; // Lista de inicializacao

vetor1[0] = 10;
vetor1[1] = 15;
vetor1[2] = 20;
vetor1[3] = 35;
vetor1[4] = 15;
```

### NOTA:

Um `array` convencional não se pode acessar todas as suas posições de uma só vez exceto em sua inicialização ao inserir valores, caso deseje acessar e imprimir os valores de cada posição, será necessário utilizar um laço de repetição e iterar por cada valor:

```java
int[] vetor1 = {10, 15, 20, 35, 15};

for (i=0; i<vetor1.length; i++){
	System.out.println(vetor1[i]);
}
```

Caso tente acessar diretamente os valores do `array` usando `System.out.println(vetor1);`, retornará apenas a referência da classe do `array` com o hash hexadecimal e a referência ao tipo do `array` no formato `[I@15aeb7ab`. “I” significando que pertence a um `array` de inteiros, seguido do seu endereço na memória.

O mesmo não ocorre se o `array` for criado com uma classe invólucro, pois desta forma estamos imprimindo o próprio objeto e retorna os valores normalmente.

## Diferenças entre Array e Lista

### Array:

Os `arrays` em Java têm um tamanho fixo que é determinado na criação e não pode ser alterado posteriormente. Se precisar de um tamanho diferente, será necessário criar um novo `array`.

Um `array` pode ser composto por tipos primitivos, como `int` ou `char`, ou por objetos, como `String` ou qualquer outra classe.

O acesso aos elementos é feito diretamente por índice, e a manipulação dos elementos é geralmente mais eficiente.

### Lista:

Listas em Java, como `ArrayList`, têm tamanho dinâmico, o que significa que podem crescer ou encolher conforme necessário.

Listas oferecem uma variedade de métodos e funcionalidades como adição, remoção, busca, ordenação e outras operações que para ajudar na manipulação de dados.

## Matrizes

É uma coleção de dados bidimensional (no mínimo) de valores do mesmo tipo de dados organizados por linhas e colunas.

Pode ser interpretado como um `array` de vetores, onde os elementos são encontrados a partir dos índices (um para linha e um para coluna), onde cada “linha” na verdade é um `array` diferente.

Exemplo em C:

```c
int matriz[3][3];

matriz[0][0] = 1;
matriz[0][1] = 2;
matriz[0][2] = 3;
matriz[1][0] = 4;
matriz[1][1] = 5;
matriz[1][2] = 6;
matriz[2][0] = 7;
matriz[2][1] = 8;
matriz[2][2] = 9;

printf("Os valores da primeira linha da matriz: \n");
printf("%d %d %d", matriz[0][0], matriz[0][1], matriz[0][2]);
```

Aqui estamos definindo uma matriz 3x3 e atribuindo manualmente os valores de cada linha e coluna e, por fim, listando a primeira linha de elementos.

Resultado:

![Example4](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo4.png?raw=true)

Assim como um vetor, podemos criar uma lista de inicialização:

```c
int matriz[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

printf("Imprimindo a primeira linha: \n");

for(int j = 0; j < 3; j++){
  printf(" %d", matriz[0][j]);
}

printf("\nImprimindo a matriz inteira: \n");

for(int i = 0; i < 3; i++){
  for(int j = 0; j < 3; j++){
    printf(" %d", matriz[i][j]);
  }
   printf("\n");
}
```

Resultado:

![Example5](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo5.png?raw=true)

Vejamos que com o uso de matrizes, os laços de repetição são bem úteis, pois é inviável atribuir ou buscar os elementos manualmente quando a matriz tem muitos elementos.

O mesmo exemplo em Java:

```java
int[][] matriz = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
// ou para setar o tamanho diretamente:
// int[][] matriz = new int[3][3];

System.out.println("Matriz: ");
for(int i = 0; i < 3; i++){
    for(int j = 0; j < 3; j++){
        System.out.print(matriz[i][j] + " ");
    }
    System.out.println();
}
```

Resultado:

![Example6](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo6.png?raw=true)

Estes exemplos também podem ser recriados usando classes invólucros:

```java
Integer[][] matriz = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
// ou
// int[][] matriz = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

for (i = 0; i < matriz.length; i++) {
    for (int j = 0; j < matriz[i].length; j++) {
        System.out.print(matriz[i][j] + " ");
    }
    System.out.println();
}
```

### Dúvidas

A forma como nós (humanos) enxergamos uma matriz é diferente de como um computador “enxerga”. Nós temos o conceito de linhas e colunas, porém a máquina interpreta as linhas como diferentes vetores, ou seja, cada linha é um vetor e as “colunas” são definidas pelos elementos das “linhas”.

Como no exemplo acima, para contar a quantidade de “linhas”, está apenas contando a quantidade de vetores que há dentro de matriz por meio de `length`. E as colunas definidas pelas quantidade de elementos de cada “linha” por meio de `[i].length`. Ou seja, 3 vetores (3 linhas) com 3 elementos cada linha, logo 3 colunas.

### Exercícios de fixação

A seguir temos dois exercícios propostos que utilizam os exemplos passados até agora.

**Exercício 1:**  criar um novo vetor, inicializar ele com quaisquer valores e criar um algoritmo que encontre o maior elemento dentro deste vetor.

```java
public static void maiorElemento(){
  byte max = 0;
  byte[] vetor = {4, 5, 10, 5, 20, 3, 10};

  for(byte i = 0; i < vetor.length; i++){
      if(vetor[i] > max){
          max = vetor[i];
      }
  }

  System.out.println("Maior elemento do seu vetor: ");
  System.out.println(max);
}
```

![Example7](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo7.png?raw=true)

**Exercício 2:** Desenvolva um algoritmo que preencha uma matriz numérica de dimensões 3x3. Após preencher toda a matriz, o usuário deve inserir uma chave de busca X.
Caso exista algum número igual a X dentro da matriz, o algoritmo deve mostrar na tela, os índices da linha e da coluna da posição na qual X foi encontrado pela primeira vez. Caso contrário, o algoritmo deve se encerrar com uma única mensagem, dizendo "chave não encontrada".

```java
public static void procuraNaMatriz(){
  byte[][] matriz = new byte[3][3];
  byte i, j, x = 0, row = 0, col = 0;
  byte found = 0;
  Scanner scanner = new Scanner(System.in);

  for (i = 0; i < matriz.length; i++) {
      for (j = 0; j < matriz[i].length; j++) {
          System.out.println("Digite o valor da linha " + i + " e coluna " + j);
          if(scanner != null) {
              matriz[i][j] = scanner.nextByte();
          }
      }
  }

  System.out.println("Digite o valor da chave que deseja encontrar na matriz: ");
  if(scanner != null) {
      x = scanner.nextByte();
  }

  for (i = 0; i < matriz.length; i++) {
      for (j = 0; j < matriz[i].length; j++) {
          if (matriz[i][j] == x) {
              row = i;
              col = j;
              found = 1;
              break;
          }
      }
      System.out.println();
  }

  if(found == 1){
      System.out.println("Chave encontrado na linha " + row + " e coluna " + col);
  } else {
      System.out.println("Chave nao encontrado na matriz.");
  }
}
```

A mesma resolução em C:

```c
#include <stdio.h>

int main(void) {
  int mat[3][3];
  int i, j, x, row, col, found = 0;

  for (i = 0; i < 3; i++) {
    for (j = 0; j < 3; j++) {
      printf("Digite o valor da linha %d e coluna %d: ", i, j);
      scanf("%d", &mat[i][j]);
    }
  }

  printf("Insira a chave de busca: \n");
  scanf("%d", &x);

  for (i = 0; i < 3; i++) {
    for (j = 0; j < 3; j++) {
      if (mat[i][j] == x) {
        row = i;
        col = j;
        found = 1;
        break;
      }
    }
  }

  if (found == 1) {
    printf("Chave encontrada na linha %d e coluna %d \n", row, col);
  } else {
    printf("Chave não encontrada \n");
  }
}
```

![Example8](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_ArraysAndLists_Exemplo8.png?raw=true)
