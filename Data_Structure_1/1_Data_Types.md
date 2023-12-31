# 1 - Tipos de dados

Entenda variáveis, tipos primitivos (inteiros, floats, booleanos, etc.) e como eles são armazenados.

- Int: número inteiro de no máximo 32 bits;
- Float: numero com ponto flutuante (números decimais) de precisão simples com 32 bits (ocupando 4 bytes na memória) e precisão de 7 casas decimais. Geralmente usado quando necessita economizar espaço na memória, porem com uma pequena imprecisão nos valores;
- Double: numero com ponto flutuante de precisão dupla, usa 64 bits (ocupa 8 bytes na memória) para precisão de 15 casas decimais. Usado geralmente quando a precisão e uma coisa critica, como cálculos financeiros e científicos;
- Boolean: dado que representa 0 ou 1 (verdadeiro ou falso), representando apenas 1 bit;
- Char: dado que presenta um caractere, ocupando 1 byte (8 bits) na memória.

Exemplo dos dados primitivos no Java:

![DataTypes](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_DataTypes_DadosPrimitivosJava.png?raw=true)

### Exemplos de uso:

```java
// Type casting quer dizer que estou especificando o tipo de dado que sera 
// salvo na memoria

// Ocupa 8 bits
byte numeroPequeno = 20; // Automatic type casting
byte numeroPequeno = (byte) 20; // Manual Type casting,
Byte numeroPequeno2 = new Byte(20);

// Ocupa 16 bits
short numeroMedio = 1000;
Short numeroMedio2 = new Short(1000);

// Ocupa 32 bits
int numeroGrande= 5000000; // Automatic type casting
int numeroGrande2 = (int) 5000000; // Manual Type casting,

// Ocupa 64 bits
long numeroMuitoGrande = 100000000000;
Long numeroMuitoGrande2 = new Long(100000000000);

// Criando um objeto da classe inteiro e passando um valor que sera 
//convertido para int
Integer numeroGrande3 = new Integer(5000000);

//Ocupa 32 bits
float salary1 = 1200.0f; // Se nao usar type casting manual, necessario o f, sem ele o java entende como double
Float salary2 = new Float(1200.0f);

// Ocupa 64 bits
double bitcoin1 = 1.213133123432;
Double bitcoin2 = new Double(1.213133123432);

char genero = 'M'; // Precisa ser com aspas simples
Char genero2 = new Char('M');

String texto = "Minha string"; // Precisa ser com aspas duplas
String texto2 = new String("Minha string 2");
```

### Incompatibilidades

Por ser fortemente tipado, o Java não permite que um tipo seja atribuído a outro de qualquer jeito, como no Javascript.

```java
int idade = 22;
String idadeEmString = idade; // errado
String idadeEmString2 = Integer.toString(idade); // correto, usando classe invólucro 
```

### Esclarecimentos:

Uma classe invólucro permite converter um tipo primitivo em um objeto, fornecendo funcionalidades adicionais para manipulação de dados.

Vejamos que neste primeiro caso, por se tratar de um dado primitivo, não temos acesso a nenhuma função para manipular este valor:

![Example](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_DataTypes_JavaExemplo1.png?raw=true)

Agora no segundo caso, estamos usando uma classe invólucro e não se trata mais de apenas um byte, mas um objeto de byte, podendo ser manipulado:

![Example](https://github.com/VitorHugoAntunes/Data_Structure_Learning/blob/main/Assets/DS1_DataTypes_JavaExemplo2.png?raw=true)

### Observações:

Em versões mais recentes do JAVA, a forma como declarar uma classe invólucro muda:

```java
// Old: 'Float(float)' is deprecated and marked for removal, since version '9'
Float salary2 = new Float(1200.0f);

// New
Float salary2 = 1200.0f;
```

### NOTA:

Por qual razão o Java tem tantos subtipos de dados primitivos e não é mais simples como o Python?

O Java é feito para rodar em diferentes ambientes e dispositivos. Uma geladeira inteligente não tem o mesmo hardware e memória de um servidor. Logo, cuidar os dados da maneira correta para economizar memória e performance é importante para manter seu código rodando bem em qualquer lugar.

### Atenção:

Apesar das diferenças de linguagem para linguagem, os dados primitivos seguem regras padronizadas. Porém não quer dizer que um dado primitivo tem as mesmas características em todas as linguagens.

Por exemplo:

```java
int var1 = 10; // Em Java, int ocupa 32 bits na memoria
```

```c
int var1 = 10; // Em C, int ocupa 16 bits na memoria
```

Ou seja, para utilizar 32 bits, assim como no Java, em C devemos usar o `long int.`

E para ter o mesmo tamanho de 16 bits do `int` em C, no Java devemos usar o `short`.

**Necessário seguir a documentação de cada linguagem ao desenvolver um projeto para evitar confusões.**
