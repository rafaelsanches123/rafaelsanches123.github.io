---
layout: post
title:  "Introdução a linguagem python parte 7 - Laços de Repetição"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Laços de repetição

Os lações de repetição são utilizados na maioria das vezes para realizar repetições que podem ser previamente conhecidas ou não dependendo do que você deseja realizar. Uma aplicação bastante realizada por meio de repetições por exemplo ocorre quando eu tenho uma lista de itens e eu desejo saber quem são todos esse itens dessa lista. Ou enquanto algo não ocorrer eu continuo repetindo algum bloco de comando até que tal condição seja satisfeita.

No python nos temos os seguintes comandos de laço de repetição sendo eles o: __for__ e o __while__.

o laço de repetição __for__: ele é geralmente utilizado quando eu sei a quantidade de repetições a serem realizadas.

o laço de repetição __while__: ele é geralmente utilizado quando eu não sei o número de repetições a serem realizadas.

Vamos entender isso um pouco mais. Vamos imaginar que o professor Rafael te passou uma lição para casa e você não a fez. Como castigo o professor Rafael lhe pediu para que escrever na losa o seu nome dele 10 vezes para que você não esqueça mais de fazer a lição de casa. Poxa vida mas que coisa chata, é verdade eu também pensei o mesmo.

No mundo digital isso não precisa ser chato basta, utilizar o laço __for__ para nos ajudar nessa tarefa. Ok mas o que eu faço? vamos lá:

```bash
>>> for i in range(0,10):
...     print("Rafael")
...
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
>>>
```
Vamos entender o código acima e também o que o comando novo que surgiu faz. A estrutura do comando for é bastante simples de forma falada o que ele faz é: "Para" cada valor "i" iniciando a partir de "0" até "10" faça. De forma bastante sucinta é exatamente isso que ele faz. O comando __range__ nada mais é do que uma __função__ algo que será visto mais a frente que cria para você uma lista de números que vai de 0 até 9 exatamente. A variável i após o comando for para cada iteração ela recebe o conteudo gerado pela função range.

Agora, vamos replicar a mesma ideia acima só que uma pitada a mais de conhecimento utilizando o comando __enumerate__ e pega uma lista ou outro tipo de coleção de dados e lhe retorna o indice e o valor referente aquele indice. Vamos por a mão na massa para entender isso melhor:

```bash
>>> numeros = range(0,10)
>>> numeros
range(0, 10)
>>> for indice, valor in enumerate(numeros):
...     print("indice:",indice,"valor:",valor)
...
indice: 0 valor: 0
indice: 1 valor: 1
indice: 2 valor: 2
indice: 3 valor: 3
indice: 4 valor: 4
indice: 5 valor: 5
indice: 6 valor: 6
indice: 7 valor: 7
indice: 8 valor: 8
indice: 9 valor: 9

>>> for indice, valor in enumerate(numeros):
...     print("indice:",indice,"valor:",valor,"Rafael")
...
indice: 0 valor: 0 Rafael
indice: 1 valor: 1 Rafael
indice: 2 valor: 2 Rafael
indice: 3 valor: 3 Rafael
indice: 4 valor: 4 Rafael
indice: 5 valor: 5 Rafael
indice: 6 valor: 6 Rafael
indice: 7 valor: 7 Rafael
indice: 8 valor: 8 Rafael
indice: 9 valor: 9 Rafael
>>>

```

No exemplo acima como ainda estamos utilizando sequência numérica o indice tem o mesmo valor que o seu conteudo. Para deixar isso mais claro vamos ver um exemplo com uma lista de frutas e exibir cada fruta e seus respectivo indice referente a sua posição na lista.

```bash
>>> lista_frutas = ['maça','pera','morango','limão','banana','uva']
>>> for fruta in lista_frutas:
...     print("Nome fruta:", fruta)
...
Nome fruta: maça
Nome fruta: pera
Nome fruta: morango
Nome fruta: limão
Nome fruta: banana
Nome fruta: uva
>>>
```

```bash
>>> for indice,valor in enumerate(lista_frutas):
...     print("posicao da fruta na lista:", indice, "Nomde da fruta:", valor)
...
posicao da fruta na lista: 0 Nomde da fruta: maça
posicao da fruta na lista: 1 Nomde da fruta: pera
posicao da fruta na lista: 2 Nomde da fruta: morango
posicao da fruta na lista: 3 Nomde da fruta: limão
posicao da fruta na lista: 4 Nomde da fruta: banana
posicao da fruta na lista: 5 Nomde da fruta: uva
>>>

```

Simples não é mesmo?

Agora vamos entender melhor o laço de repetição __while__. O comando __while__ faz com que um conjunto de instruções seja executado enquanto uma condição é atendida. Quando o resultado dessa condição passa a ser falso, a execução do loop é interrompida, como mostra o exemplo a seguir.

```bash
>>> contador = 0
>>> while (contador < 10):
...        print(contador)
...        contador   = contador + 1
...
0
1
2
3
4
5
6
7
8
9
```
No código acima eu inicializei uma variável chamanda de contador com o valor zero e na linha seguinte eu uso o comando while seguido de uma expressão booleana que enquanto ela continuar sendo verdadeira o laço de repetição irá continuar acontecendo. No caso do exemplo acima a condição diz que __ENQUANTO__ o conteúdo da variável contador for menor que dez o laço de repetição deve ser executado.
Nesse exemplo a cada execução é apresentado ao usuário o valor corrente da variável contador naquele momento e na sequência ele tem seu valor alterado para que em determinado momento o laço seja interrompido e por consequência finalizado. Se por algum acaso a sua condição sempre gerar resultado verdadeiro você irá cair no que chamamos de loop infinito ou laço de repetição sem fim. Evite que isso aconteça, pois leva ao congelamento e finalização da aplicação/programa de computador.

A seguir veja um exemplo utilizando entrada de dados.

```bash
>>> numero = int(input("Informe um número entre 1 a 10\n"))
Informe um número entre 1 a 10
2
>>> while(numero > 0 and numero <=10):
...     print("Você informou o número: {}".format(numero))
...     numero = int(input("Informe um número entre 1 a 10\n"))
...
Você informou o número: 2
Informe um número entre 1 a 10
2
Você informou o número: 2
Informe um número entre 1 a 10
5
Você informou o número: 5
Informe um número entre 1 a 10
0

```
Veja que interessante o código acima. Nele é solicitado um número ao usuário e enquanto esse número informado pelo usuário for maior que zero e menor ou igual a dez o computador irá ficar solicitando ao usuário um número desde que ele atenda a condição do laço while.

```bash
>>> numero = int(input("Informe um número entre 1 a 10\n"))
Informe um número entre 1 a 10
1
>>> print(numero)
1
>>> while(numero > 0 and numero <=10):
...     print("Você informou o número: {}".format(numero))
...     numero = int(input("Informe um número entre 1 a 10\n"))
... else:
...     print("Você informou o número: {} e ele está fora da condição estabelecida".format(numero))
...
Você informou o número: 1
Informe um número entre 1 a 10
5
Você informou o número: 5
Informe um número entre 1 a 10
6
Você informou o número: 6
Informe um número entre 1 a 10
4
Você informou o número: 4
Informe um número entre 1 a 10
11
Você informou o número: 11 e ele está fora da condição estabelecida

```

O código acima é exatamente igual ao anterior mas com o diferencial do comando __else__ eu particularmente nunca utilizei ele com laço de repetição while mas, se em algum momento você precisar fica ai mais uma forma de utilizar ele no seu dia a dia se for da sua vontade e necessidade.

Exercícios para praticar o que aprendeu:

1. Com a ajuda de uma laço de repetição, solicite ao usuário um número inteiro e a cada iteração desse laço. O número de repetições deve ser 10. A cada iteração imprimir na tela a sequência do laço e o número que o usuário informou naquela iteração.

2. Faça um programa similar ao programa do exercício 1 acima. Nesse novo programa, ao final da execução desse laço de repetição você precisa imprimir na tela do usuário qual foi o menor número informado durante a execução do laço de repetição.

3. Faça um programa similar ao programa do exercício 2 acima. Nesse novo programa, ao final da execução desse laço de repetição você precisa imprimir na tela do usuário qual foi o maior número informado durante a execução do laço de repetição.

4. Solicite ao usuário dois números inteiros e imprimir na tela do usuário os números entre os dois números solicitados. Ex: n1=2 e n2=5 caso você use esses dois número o deverá aparecer na tela do usuário a seguinte sequência: 2, 3, 4, 5.

5. Faça um programa similar ao programa do exercício 4 acima. Nesse novo programa, você deve imprimir no final da sequência solicitada ao usuário o somatório dessa sequência.

6. Com a ajuda de um laço de repetição realize 20 repetições e imprima na tela do usuário somente as posições impares.

7. Com a ajuda de um laço de repetição realize 30 repetições e imprima na tela do usuário somente as posições pares.

8. Com a ajuda de um laço de repetição, fique solicitando um valor inteiro ao usuário a cada iteração do laço. O laço de repetição nesse exercício só deve terminar quando o usuário informar um valor inteiro negativo.

9. Desenvolva um programa gerador de tabuada, capaz de gerar a tabuada de qualquer número inteiro entre 1 a 10. O usuário deve informar de qual numero ele deseja ver a tabuada. A saída deve ser conforme o exemplo abaixo:
Tabuada de 5:
5 X 1 = 5
5 X 2 = 10
...
5 X 10 = 50

10. O desafio mais dificil desse estágio: __Fibonacci__ é uma sequência de números, que aparece em certos mistérios da natureza e da vida, onde a sequência inicia com 0 e 1, e os números seguintes serão a soma dos dois números anteriores.

Por exemplo: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55…

Faça um programa capaz de gerar a série de Fibonacci até o n−ésimo termo ou seja, solicite um número inteiro ao usuário e dado esse número gerar a série de Fibonacci até essa posição da sequência. Por exemplo, se o usuário solicitar a 7ª você deve gerar a sequência 0, 1, 1, 2, 3, 5, 8 na tela do usuário.
