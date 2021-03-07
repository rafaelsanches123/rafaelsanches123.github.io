---
layout: post
title:  "Introdução a linguagem python parte 9 - Estruturas de Dados"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Estruturas de dados

Estruturas de dados consistem na organização de dados na memória de um computador ou em um dispositivo de armazenamento de modo que esses dados possam ser acessados de forma performática.

Em python temos estruturas de dados por meio dos tipos de variáveis compostas __Listas__, __Dicionários__, __Tuplas__ e __Conjuntos__ que nos auxiliam de forma performática a armazenar dados e acessá-los da melhor forma possível. Vale ressaltar que isso ocorre de modo mais alto nível em comparação a linguagens como a __c__ por exemplo que você desenvolve todo processo relacionado a essas estruturas de dados desde a conexão entre posições na memória por meio de ponteiros e a lógica por trás desses processos que precisam ser desenvolvidos.

### Tupla:

A tupla é uma variável de tipo composto que permite que seja atribuído a ela mais de um tipo de variável simples/primitiva. Isso é básicamente uma lista que vai guardar variáveis porém, existe um ponto importante sobre tuplas, elas não permitem ser modificadas depois de serem criadas ou seja a __Tupla__ é uma Lista __imutável__. Veja o exemplo a seguir:

Código:
```python
nomes = ("Rafael", "Gabriel", "Pedro")

print(nomes[0])
print(nomes[1])
print(nomes[2])

print(type(nomes))

nomes[0] = "Leandro"

```
Resultado:
```bash
Rafael
Gabriel
Pedro
<class 'tuple'>
Traceback (most recent call last):
  File "main.py", line 9, in <module>
    nomes[0] = "Leandro"
TypeError: 'tuple' object does not support item assignment
>>>

```
No resultado ilustrado acima é possível visualizar a imutabilidade de uma tupla quando tentamos alterar ela.

Uma tupla pode ser declada das seguintes formas a baixo:

```python
# Tupla declarada sem o uso de parêntesis
tupla_1 = 1, 2, 3
# Tupla declarada com o uso de parêntesis
tupla_2 = (1, 2, 3)

# Tupla com um único elemento
tupla_3 = 1,

# Tupla vazia
tupla_4 = ()
```

Durante meus anos de desenvolvimento eu particularmente não cheguei a precisar utilizar tupla nos softwares que já criei. Se você que está lendo esse post já teve que utilizar para algo comenta nos comentários onde você já utilizou!


### Lista:

As listas em Python são uma sequência ordenada de valores onde, cada valor na lista é identificado por um índice. Os valores que formam uma lista são chamados elementos ou itens. Listas são similares a strings, que são uma sequência de caracteres, no entanto, diferentemente de strings, os itens de uma lista podem ser de tipos diferentes e tamanhos.

Veja um exemplo na imagem a seguir:

![lista-em-python]({{ site.url }}/assets/listas-em-python.png){:style="width: 100%" }

***Figura 1***: *Exemplo do tipo de dados lista em python*

Na Figura acima é possível observar um exemplo de lista na qual ela tem tamanho 6. Vale lembrar que em python as listas começam na posição 0. Na lista de exemplo na imagem é possível observar que ela tem o número 29 do tipo inteiro na 1ª posição. Na 2ª posição temos o nome Rafael que nada mais é do que uma variável do tipo String. Na 3ª posição temos o número -9. Na 4ª posição temos a string cursos. Na 5ª posição temos uma lista de números inteiros e na última posição (i.e., 6ª) temos um tipo string contendo a palavra Teste.

Uma coisa que geralmente deixa as pessoas confusas quando estão aprendendo alguma linguagem de programação é a posição dos elementos. Isso ocorre pelo fato de começarem pela posição 0 e não pela posição 1. Não se preocupe que com o tempo você se acostuma com isso e vai virar algo super comum para você.

Bora ver alguns exemplos de como criar listas e algumas ações que podemos realizar sobre elas.

Primeiro passo é criar uma lista:
```python
#Lista vazia
lista1 = []

#Lista da Figura 1
lista2 = [29,"Rafael",-9,"cursos",[1,2,3,4,5],"Teste"]
```
Para descobrirmos a quantidade de elementos em uma lista pode usar a função __len__:

```python
#Tamanho de uma lista
print("O tamanho da lista1 é: {}".format(len(lista1)))

print("O tamanho da lista2 é: {}".format(len(lista2)))
```

Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
O tamanho da lista1 é: 0
O tamanho da lista2 é: 6
```
Para acessar os elementos de uma lista podemos realizar essa ação de dois modos, um deles seria acessando o elemento na posição desejada e o outro por meio de um laço de repetição.

Exemplos utilizando laço de repetição:

```python
#iterar sobre uma lista
for elemento in lista2:
  print("Elemento: {}".format(elemento))
```
```bash
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
Elemento: 29
Elemento: Rafael
Elemento: -9
Elemento: cursos
Elemento: [1, 2, 3, 4, 5]
Elemento: Teste
```
```python
#exibir posição e elemento daquela posição
for posicao, elemento in enumerate(lista2):
  print("Posição: {}, Elemento: {}".format(posicao, elemento))
```

Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Posição: 0, Elemento: 29
Posição: 1, Elemento: Rafael
Posição: 2, Elemento: -9
Posição: 3, Elemento: cursos
Posição: 4, Elemento: [1, 2, 3, 4, 5]
Posição: 5, Elemento: Teste
```
Veja agora alguns exemplos acessando diretamente a posição de uma lista:

```python
print(lista1[0])
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Traceback (most recent call last):
  File "main.py", line 27, in <module>
    print(lista1[0])
IndexError: list index out of range
```
Para o exemplo acima a lista1 esta vazia logo, não é possível acessar nada nela e por isso ao tentarmos acessar uma posição qualquer nela ela gerou a exceção acima na saída do código. Lembre se que mesmo para uma lista que contenha elementos e não esteja vazia se você tentar acessar uma posição que não exista nessa lista a exceção acima também ocorrerá.

```python
#Posição 0
print(lista2[0])

#Posição 3
print(lista2[2])

#Posição 5
print(lista2[4])
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
29
-9
[1, 2, 3, 4, 5]
```

Se eu quiser verificar se um determinado elemento está na lista eu posso utilizar o operador __in__:
```python
if(-9 in lista2):
  print("-9 está na lista2 !")
else:
  print("-9 não está na lista2 !")
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
-9 está na lista2 !
```
```python
if(30 in lista2):
  print("30 está na lista2 !")
else:
  print("30 não está na lista2 !")
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
30 não está na lista2 !
```

Sabia que você também pode encontrar valores de mínimos, máximos e soma utilizando listas:

```python
#lista composta somente por números
lista3 = [10, 5, 3, 18, 1, 25]

#mínimo
print("Menor valor: {}".format(min(lista3)))

#máximo
print("Maior valor: {}".format(max(lista3)))

#somatório
print("Soma: {}".format(sum(lista3)))
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Menor valor: 1
Maior valor: 25
Soma: 62
```




```python
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
```

Em desenvolvimento...

### Dicionário:
Em desenvolvimento...
```python
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
```

### Conjunto:
Em desenvolvimento...
```python
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
```
