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

A ordenação de listas:

```python
#ordem crescente
print(sorted(lista3, key=int, reverse=False))

#ordem decrescente
print(sorted(lista3, key=int, reverse=True))
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
[1, 3, 5, 10, 18, 25]
[25, 18, 10, 5, 3, 1]
```

Operações com Listas:

```python
#Adicionando elementos de forma dinâmica a listas:

#lista vazia
lista_nomes = []

#adicionando nomes a lista vazia

#adicionando elemento na última posição da lista
lista_nomes.append("Rafael")

#adicionando elemento na última posição da lista
lista_nomes.append("Francisco")

#adicionando elemento na última posição da lista
lista_nomes.append("Viana")

#adicionando elemento na última posição da lista
lista_nomes.append("Sanches")

#exibindo a lista
print(lista_nomes)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
['Rafael', 'Francisco', 'Viana', 'Sanches']
```

A função __append__ sempre insere elementos no final da lista. Isso é bom por questões de desempenho. É mais rápido inserir elementos no final de uma lista porque não precisamos percorrer a lista procurando a posição onde o elemento deve ser inserido. Mas também é possível inserir elementos em posições específicas da lista, usando a função __insert__.


```python
lista_nomes.insert(1, "Teste")

#exibindo a lista
print(lista_nomes)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
['Rafael', 'Teste', 'Francisco', 'Viana', 'Sanches']
```

Removendo elementos de listas:

```python
#lista vazia
lista_nomes = []

#adicionando nomes a lista vazia

#adicionando elemento na ultima posição da lista
lista_nomes.append("Rafael")

#adicionando elemento na ultima posição da lista
lista_nomes.append("Francisco")

#adicionando elemento na ultima posição da lista
lista_nomes.append("Viana")

#adicionando elemento na ultima posição da lista
lista_nomes.append("Sanches")

#exibindo a lista original
print("Lista Original: ",lista_nomes)

lista_nomes.remove("Viana")

#exibindo a lista
print("Lista Modificada: ",lista_nomes)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Lista Original:  ['Rafael', 'Francisco', 'Viana', 'Sanches']
Lista Modificada:  ['Rafael', 'Francisco', 'Sanches']
```

Para remover um elemento em uma posição específica, usamos a função __del__. Observe a diferença em relação à função remove, que recebe como parâmetro o valor que desejamos remover.

```python
#lista vazia
lista_nomes = []

#adicionando nomes a lista vazia

#adicionando elemento na ultima posição da lista
lista_nomes.append("Rafael")

#adicionando elemento na ultima posição da lista
lista_nomes.append("Francisco")

#adicionando elemento na ultima posição da lista
lista_nomes.append("Viana")

#adicionando elemento na ultima posição da lista
lista_nomes.append("Sanches")

#exibindo a lista original
print("Lista Original: ",lista_nomes)

del lista_nomes[3]

#exibindo a lista
print("Lista Modificada: ",lista_nomes)

```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Lista Original:  ['Rafael', 'Francisco', 'Viana', 'Sanches']
Lista Modificada:  ['Rafael', 'Francisco', 'Viana']
```

Exitem ainda muitos outros métodos que podemos utilizar com listas e para poder conhece-los abra seu terminal e digite o comando __help(list)__. Segue um exemplo:

```bash
Python 3.8.5 (default, Jan 27 2021, 15:41:15)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> help(list)
```

### Dicionário:

Os dicionários são estruturas que não possuem uma ordenação específica. Os dicionários são representados na forma de chave e valor. A chave é uma referência para o valor de um elemento do dicionário. Veja a seguir alguns exemplos de ações que você pode realizar com dicionários.

Os dicionários são criados colocando os pares __chave__ : __valor__ entre chaves __{__ __}__ da seguinte forma:

Criando um dicionário:

```python
#dicionário vazio
dicionario = {}

#imprimindo o conteúdo do dicionário
print("Dicionário vazio: ",dicionario)

#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

#acessando itens de um dicionário
print(dicionario['Rafael'])
print(dicionario['Renata'])
print(dicionario['Ana'])
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Dicionario vazio:  {}
PYTHON
SQL
PHP
```

Para recuperar um valor no dicionário podemos usar o método __get__ passando como argumento a chave do valor que queremos recuperar:

```python
#dicionário criado com chave e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

#imprimindo o conteúdo das chaves Rafael, Renata e Ana usando o método get
print(dicionario.get('Rafael'))
print(dicionario.get('Renata'))
print(dicionario.get('Ana'))
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
PYTHON
SQL
PHP
```

Iterando sobre os itens de um dicionário utilizando o laço de repetição __for__:

```python
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

for chave in dicionario:
  print(chave, 'programa em:', dicionario[chave])
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Rafael programa em: PYTHON
Renata programa em: SQL
Joao programa em: JAVA
Bruno programa em: C++
Ana programa em: PHP
```

Para alterar uma valor em um dicionário use o nome do dicionário com a chave entre colchetes e associe um __novo valor__ a __chave__:

```python
#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

print("Antes da alteração: ",dicionario)

dicionario['Rafael'] = 'Ruby'

print("Depois da alteração: ",dicionario)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Antes da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
Depois da alteração:  {'Rafael': 'Ruby', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
```

Para inserir um novo item em um dicionário basta declarar o dicionário colocando entre colchetes a __nova chave__ e __atribuindo um valor a ela__:

```python
#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

print("Antes da alteração: ",dicionario)

dicionario['Joelson'] = 'C#'

print("Depois da alteração: ",dicionario)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Antes da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
Depois da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP', 'Joelson': 'C#'}
```

Inserindo itens novos ou alterando itens já existentes em um dicionário com o método __update()__.

```python
#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

print("Antes da alteração: ",dicionario)

# Chave não existe no dicionario. Nesse caso ocorre automaticamente uma inserção no dicionário ou seja, um novo conjunto de chave e valor é adicionado ao dicionário.
dicionario.update({'Joelson':'C#'})

print("Depois da alteração: ",dicionario)

# Chave já existe no dicionario. Nesse caso ocorre automaticamente uma atualização no dicionário ou seja, um novo valor é atribuído a uma chave que já está no dicionário.

dicionario.update({'Rafael':'R'})

print("Depois da alteração: ",dicionario)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Antes da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
Depois da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP', 'Joelson': 'C#'}
Depois da alteração:  {'Rafael': 'R', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP', 'Joelson': 'C#'}
```

Removendo um par chave e valor de um dicionário usando o comando __del__:

```python
#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

print("Antes da alteração: ",dicionario)

del dicionario['Bruno']

print("Depois da alteração: ",dicionario)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Antes da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
Depois da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Ana': 'PHP'}
```

Removendo e obtendo um par chave, valor com o método __pop()__:

```python
#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

print("Antes da alteração: ",dicionario)

dicionario.pop('Renata')

print("Depois da alteração: ",dicionario)
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Antes da alteração:  {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
Depois da alteração:  {'Rafael': 'PYTHON', 'Joao': 'JAVA', 'Bruno': 'C++', 'Ana': 'PHP'}
```

Para poder entender o seu dicionário ou o dicionário que outra pessoa tenha criado, você pode usufruir de alguns métodos sendo eles:

Nome do método | O que ele faz?
:------:|:------:
keys() | Ele retorna todas as chaves de um dicionário
values() | Ele retorna todos os valores de um dicionário
items() | Ele retorna todos os pares de chave e valor de um dicionário


```python
#dicionário criado com chaves e valores
dicionario = {'Rafael': 'PYTHON', 'Renata': 'SQL', 'Joao' : 'JAVA', 'Bruno': 'C++', 'Ana' : 'PHP'}

print("Todas as chaves: ",dicionario.keys())
print("Todos os valores: ",dicionario.values())
print("Todos os pares de (chave, valor): ",dicionario.items())

```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
Todas as chaves:  dict_keys(['Rafael', 'Renata', 'Joao', 'Bruno', 'Ana'])
Todos os valores:  dict_values(['PYTHON', 'SQL', 'JAVA', 'C++', 'PHP'])
Todos os pares de (chave, valor):  dict_items([('Rafael', 'PYTHON'), ('Renata', 'SQL'), ('Joao', 'JAVA'), ('Bruno', 'C++'), ('Ana', 'PHP')])
```

Vale ressaltar que os comandos utilizados acima retornam para o método __keys()__ uma lista com as chaves existentes no dicionário. Para o método __values()__, retorna-se uma lista com os valores do dicionário. O método __items()__ ele é um pouco diferente pois ele retorna uma lista que seus elementos por sua vez possuem tuplas como valores onde o primeiro elemento de cada tupla representa a chave e o segundo elemento o valor relacionado a respectiva chave do primeiro elemento.


### Conjunto:
Em desenvolvimento...
```python
```
Para o bloco de código acima teríamos a seguinte saída em nosso terminal:
```bash
```
