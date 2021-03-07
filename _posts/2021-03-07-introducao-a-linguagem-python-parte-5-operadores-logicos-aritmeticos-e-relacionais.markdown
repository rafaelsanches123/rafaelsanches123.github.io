---
layout: post
title:  "Introdução a linguagem python parte 5 - Operadores Lógicos, Aritméticos e Relacionais"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Operadores Lógicos, Aritméticos e Relacionais

__Operadores Lógicos__:
As linguagens de programação, utilizam os conectivos lógicos da lógica formal, ou melhor da lógica Aristotélica, na construção de expressões lógicas. Existem 2 conectivos lógicos e, mesmo que não os conheçamos com o nome de conectivos lógicos, utilizamo-os constantemente ao conversarmos ou então, para explicarmos qualquer disciplina a outra pessoa.

Os dois conectivos lógicos são:

Conectivo de __conjunção__: __E__
Conectivo de __disjunção__: __OU__

Os operadores lógicos são utilizados para avaliar o resultado de uma expressão ou sub-expressões de modo que seja retornado como resposta True (verdadeiro) ou False (falso) de acordo com a relação apresentada.

Veja nas tabelas a seguir um exemplo dos resultados dos operadores __AND__ e __OR__ de acordo com a tabela verdade respectiva de cada um.

__AND__:

Expressão 1 | Operador | Expressão 2 | Resultado
:------:|:------:|:------:|:------:
True | AND | True  | True
True | AND | False | False
False | AND | True | False
False | AND | False | False


__OR__:

Expressão 1 | Operador | Expressão 2 | Resultado
:------:|:------:|:------:|:------:
True | OR | True  | True
True | OR | False | True
False | OR | True | True
False | OR | False | False

Exemplos:
1. Nesse exemplo a primeira expressão e a segunda resultam em resultado verdadeiro logo, a resposta será verdadeira. O operador __AND__ só irá gerar uma resposta falsa se pelo menos uma das expressões resultar falso. Ele sempre retornará verdadeiro se todas as expressões ou sub-expressões forem verdadeiras.
```bash
>>> x = 1
>>> ((x > 0) and (x < 100))
True
>>> ((x > 1) and (x < 100))
False
```
2. Nesse exemplo a segunda expressão é falsa logo a resultado final é verdadeiro. O operador __OR__ só retornará falso quando todas expressões resultarem em falso.
```bash
>>> x = 10
>>> ((x < 1) or (x < 100))
True
>>> ((x < 1) or (x < 5))
False
```
Outros dois operadores lógicos ainda não mencionados mas, muito utilizados no python são: __not__ e o __in__. O operador not é geralmente utilizado para negar uma expressão booleana por exemplo:

```bash
>>> A = True
>>> not A
False
>>> A
True
>>> B = False
>>> B
False
>>> not B
True
>>>

```

Muito simples não é mesmo?

O operador in ele é uma ferramenta muito interessante quando temos que verificar se algo existe ou não dentro de alguma variável de tipo heterogênea como strings, listas, etc...

Vamos ver ele na prática como funciona e ver como ele é simples:

```bash
>>> lista_frutas = ['uva','maçã','limão','jaca']
>>> 'uva' in lista_frutas
True
>>> 'laranja' in lista_frutas
False
>>> frase = "eu trabalho na empresa serasa e gosto de computadores"
>>> 'empresa' in frase
True
>>> 'valor' in frase
False
>>> 'Rafael' in frase
False
>>> 'computador' in frase
True
>>> 'computaçao' in frase
False
>>>

```

__Operadores Aritméticos__:
O python é uma ferramenta tão poderosa pode ser utilizado como uma calculadora matemática avançada. Praticamente, todos os operadores aritméticos funcionam da mesma forma como os conhecemos da matemática elementar. Por exemplo, para trabalharmos com as 4 principais funções matemáticas, a soma, subtração, multiplicação e divisão, temos os operadores conforme tabela a seguir.

Operação | Operador
:------:|:------:
adição        |	+
subtração     |	-
multiplicação |	*
divisão       |	/

Além dos operadores supracitados existem também, operadores para exponenciação, obtenção da parte inteira de uma divisão, extração do módulo da divisão, conforme pode ser visto na tabela a seguir:

Operação |	Operador
:------:|:------:
exponenciação |	**
parte inteira |	//
módulo |	%

Exemplos:
Adição:
```bash
>>> 1 + 1
2
```
Subtração:
```bash
>>> 7 - 5
2
```
Multiplicação:
```bash
>>> 2 * 2
4
```
Divisão:
```bash
>>> 10/3
3

>>> 10.0/3.0
3.3333333333333335

```
Exponenciação:
```bash
>>> 2 ** 3
8

```
Parte Inteira:
```bash
>>> 10.0/4.0
2.5

>>> 10.0//4.0
2.0

```
Módulo:
```bash
>>> 10.0 % 4.0
2.0
>>> 10.0 % 2.0
0.0
>>>

```

__Operador Relacionais__:
É todo operador que obtém a relação do membro a esquerda com o membro a sua direita. Na tabela abaixo, temos os operadores relacionais disponibilizados pelo python.

Descrição |	Operador
:------:|:------:
Maior que |	>
Menor que |	<
Igual a | ==
Diferente a | !=
Maior ou igual a |	>=
Menor ou igual a |	<=

Exemplos:
```bash
>>> 10 > 2
True

>>> 10 < 2
False

>>> 10 == 2
False

>>> 10 != 2
True

>>> 10 >= 2
True

>>> 10 <= 2
False

```

Exercícios para praticar o que aprendeu:

1. Criar uma variável e chamada de __maior_valor__ e atribuir a ela o valor 10. Criar uma variável e chamada de __menor_valor__ e atribuir a ela o valor 3.

2. Usando o operador de __igual a__ verificar se o valor de __maior_valor__ é igual ao conteúdo da variável __menor_valor__.

3. Usando o operador de __diferente a__ verificar se o valor de __maior_valor__ é igual ao conteúdo da variável __menor_valor__ ou se os valores são diferentes.

4. Usando o operador __maior que__ verificar se o valor de __maior_valor__ é maior que o conteúdo da variável __menor_valor__.

5. Usando o operador __menor que__ verificar se o valor de __maior_valor__ é menor que o conteúdo da variável __menor_valor__.

6. Usando o operador __subtração__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

7. Usando o operador __multiplicação__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

8. Usando o operador __divisão__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

9. Usando o operador __parte inteira__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

10. Usando o operador __módulo__ calcular o resultado entre  __maior_valor__ e o número 2 e verificar se o resultado gerado é diferente de zero. (Se o resultado gerado for zero significado que __maior_valor__ é par).

11. Usando o operador __módulo__ calcular o resultado entre  __menor_valor__ e o número 2 e verificar se o resultado gerado é diferente de zero. (Se o resultado gerado for zero significado que __menor_valor__ é par).

12. Crie um lista de comprar e nela adicione 5 produtos que você costuma comprar no mercado. Usando o operador __in__ use 3 produtos que você não adicionou na sua lista e depois faça a mesma coisa para 2 produtos que você colocou na sua lista.

13. Utilizando o operador __not__ aplique ele para o valor 1 e depois para o valor zero e veja o que ele retorna para cada um desses valores.
