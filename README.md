# Estrutura de dados

Neste repositório deixarei algumas explicações do lado téorico da disciplina estrutura de dados I
<br><br>

<h2>Vetores e Matrizes</h2>

Vetor -> Coleção dee variáveis do mesmo tipo, acessíveis com um único nome e armazenado no instante na memória. A individualização de cada elemento do vetor é feita através dos índices.
Exemplo:

```c
#include <stdio.h>

int main(void) {
  int vetor[5]; // inicializando o vetor
  // adicionar valores de 1 até 5 no vetor
  for(int i = 0; i < 5; i++) {
    vetor[i] = i + 1;
  }
  // mostrar o vetor
  for(int i = 0; i < 5;i++) {
    printf("%d ", vetor[i]);
  }
  return 0;
}
```

Matrizes -> Matriz é uma coleção de valores que podemos armazenar em número de linhas e colunas. Temos diversos tipos de matrizes (bidimensionais, tridimensionais, n-dimensionais...).
Alguns dos tipos de matrizes:
<br>
- Matriz linha: Possui somente uma linha.
- matriz coluna: possui somente uma coluna.
- Matriz nula: Todos seus elementos são zero.
- Matriz quadrada: Número de colunas é igual ao número de linhas, comun de ordem 2.
- Matriz diagonal: Matriz quadrada onde todos os elementos que não pertecem a diagonal principal são nulos.
- Matriz identidade: Matriz diagonal porém na diagonal principal os elementos são todos 1.
- Matriz oposta: Matriz que troca os sinais dos elementos. M -> -M
- Matriz transporta: Troca de linhas por colunas.

As principais usadas na programação são:
 - Matrizes bidimensionais: Matriz quadrada de ordem 2. Exemplo:
 ```c
 #include <stdio.h>

int main(void) {
  int matriz[2][2]; //Cij; i = linhas; j = colunas
  // obteremos a seguir -> [ 2 7 ]
  //                       [ 4 1 ]
  matriz[0][0] = 2;
  matriz[0][1] = 7;
  matriz[1][0] = 4;
  matriz[1][1] = 1;
  //impressão da matriz
  for(int i = 0; i < 2;i++) {
    for(int j =0; j < 2;j++) {
      printf("%d ", matriz[i][j]);
    }
    printf("\n");
  }
  return 0;
}
 ```

- Matrizes tridimensionais: ``` int matriz [4][4][4]``` -> Neste caso é igual a bidimensional porem se usa com 3 for para entrar dentro de toda a matriz.
- N-dimensionais: são as demais ordem. Exemplo de ordem 5 -> ```int matriz [4][4][4][4][4]```, e assim por diante...
<br>
<h2>Buscas em estruturas lineares</h2>
Busca serve para nós encontrarmos um valor no vetor ou somente verificar se ele existe.
<br>

Temos 2 tipos de busca:
- Busca sequencial ou linear
- Busca binária

busca sequencial ou linear: O algoritmo percorre o vetor da primeira posição até a última, pois em cada posição verifica se vetor[i] é igual a i, se chegarmos ao fim o valor não existe. Eficiência:
 - 1 vez no melhor caso
 - n vezes pior caso ( pois ele percorreria todos elementos, imagina se tiver 100000 elementos...)
 - n / 2 no caso médio.
 ```c
 #include <stdio.h>

int main(void) {
  int vetor[5];
  for(int i = 0; i < 4;i++) {
    vetor[i] = i + 1;
  }
  int valor = 4;
  int encontrado = 0; // falso
  int i = 0;
  while (i < 5 && !encontrado) {
    if (vetor[i] == valor) {
      encontrado = 1; /*Verdadeiro*/ 
    } else {
      i++; 
    }
  }
  if (encontrado) { 
    printf ("Valor %d está na posicao %d\n", vetor[i], i);
  } else { 
    printf ("Valor %d não encontrado\n", valor);
  }
  return 0;
}
 ```

 Busca Binária: Primeiramente para fazer este tipo de busca, a lista deve estar ordenada, pois com isso ele tenta buscar o elemento pelo valor do meio da lista e se for menor ele corta os elementos da direita, se caso for maior corta os da esquerda até o valor do meio ser igual ou não encontrar. Eficiência:
 - Pior caso: log2(n) vezes.
 - 1 vez ( valor mediano do vetor )
 - log2 (n) tambem no caso médio.

 ```c
 #include <stdio.h>

int main(void) {
  int vetor[5];
  for(int i = 0; i < 4;i++) {
    vetor[i] = i + 1;
  }

  int direita, esquerda, meio; 
  int encontrado = 0; /*Falso*/ 
  esquerda = 0; 
  direita = 5 - 1; // tamanho - 1

  int valor = 3;
  while(esquerda<=direita && !encontrado){
    meio=(direita+esquerda)/2;
    if (vetor[meio] == valor) encontrado = 1; /*Verdadeiro*/
    else if (valor < vetor[meio]) direita = meio - 1;
    else esquerda = meio + 1; 
  }

  if(encontrado){
    printf ("Valor %d encontrado na posicao %d\n", vetor[meio], meio);
  } else { 
    printf ("Valor %d n~ao encontrado\n", valor);
}

  
  return 0;
}
 ```
 <br>
<h2>2 Métodos de ordenação populares nas estruturas de dados</h2>

A ordenação consiste em organizar em ordem crescente ou decrescente a sua coleção de dados para facilitar as buscas e pesquisas das ocorrências de um determinado conjunto ordenado.
<br>

Método por inserção: Metodologia de organizar as cartas do baralho, ou seja ele tira a carta do monte e inseri na posição da sequência. No caso ele pega o valor atual e compara com os elementos anteriores e se for menor troca de posição até chegar no limite ou for maior.

Método por seleção: Ele percorre o vetor e seleciona o menor elemento do vetor, depois o segundo, depois o terceiro e assim por diante.
<br>

<h2>Recursividade</h2>

A idéia do algoritmo de recursividade é recorrer a si mesmo ( chamar a si mesmo ), até resolver o problema de uma forma mais simples e um problema menor. Quando não precisa a recorrer a si mesmo está deve ser a condição de parada e o problema resolvido.
- Recursão direta: Quando uma função chama a si mesma diretamente. Exemplo:
```c
#include <stdio.h>

int main(void) {
  int imprimirDezPares(int p) {
    if (p < 20) {
      printf("%d \t",p);
      imprimirDezPares(p + 2);
    }
  }
  imprimirDezPares(0); 
  return 0;
}
```

- Recursão indireta: Quando uma função chama outra função e esta função chama a primeira.
```c
#include <stdio.h>

int main(void) {
  int imprimirDezPares(int p) {
      printf("%d \t", p);
      trocaPar(p);
  }
  int trocaPar(int p) {
    if (p < 20) {
      imprimirDezPares(p + 2);
    }
  }
  imprimirDezPares(0); 
  return 0;
}
```
<br>

<h2>Listas</h2>

São estruturas que permitem as operações de inserção remoção e recuperação de itens, sendo que as posições para as listas não importam ou signifiado para os dados. Nela importa se o dado etá ou não na lista.
 - No caso dela, os dados são adicionados verificando se tem espaço ou não, caso tenha ele insere na lista.
 - Já no processo de remoção, você pode apagar todos elementos ou somente um passando a chave dele e aquele espaço ficara NULL.

Temos alguns tipos de listas
- Listas estásticas: Possuem determinada quantidade de itens.
- Listas dinâmicas: São alocadas na memória e dependem só da memória total disponível.
- Listas ordenadas: Lista em ordem crescente ou descrescente.
- Buscas em listas: podemos usar conforme nosso aprendizado a busca sequêncial (Linear) ou se tiver ordenada a bionária.

<br>

<h2>Pilhas - Stack</h2>

Semelhante a uma pilha de pratos sujos, usa o tipo LIFO (LAST-IN FIRST-OUT), ou seja último a ser inserido é o primeiro a ser retirado. Exemplos de pilhas: Recursividadem, mecanismo de desfazer/refazer os editores de texto, navegações de página Web, entre outros. Pode ser realizadoem um vetor.

Na pilha, a manipulação dos elementos é realizada em apenas uma das extremidades, chamada de ```TOPO```, pois ele só trabalha com o Topo a pilha e não a Base.

Lembre-se da pilha como empilhar e desempilhar....
<br>

<h2>FILAS - Queue</h2>

Estruturas do tipo FIFO (first-in first-out), primeiro elemento a ser inserido é o primeiro a ser retirado, pense numa fila de banco, o primeiro a chegar é o primeiro a ser atendido e retirado da fila. O que se faz na realidade é indicar quem é o primeiro elemento.

Na realidade a remoção de elemento da fila é realizada em apenas alterando a informação da posição do ultimo elemento, resultando numa fila circular.

<h2>Principal diferença entre as 3 (Listas, pilhas e filas)</h2>

Primeiramente, vamos exemplificar ainda mais as três estururas em exemplos comuns no nosso dia a dia. 
- Lista -> Lista de compras (não importa a posição e sim se os elementos estão ali na lista).
- Pilha -> Pilha de roupas.
- Fila -> Fila de lotérica ou no caixa do Supermercado.

Ou seja, a lista não ele é a menos restrita possível, podemos trabalhar com ela em qualquer posição, pois não importa e sim o que contém nela.

Já na pilha trabalhamos sempre com o Topo, adicionamos elementos ao topo e removemos o ultimo elemento adicionado no topo.

Agora na fila é mais restrita possível, pois podemos adicionar elemento mas na remoção só indicaremos quem é o primeiro e o último elemnto e não tiraremos da memória completamente pois é estática esse tipo de listagem e restrita conforme comentado. 
