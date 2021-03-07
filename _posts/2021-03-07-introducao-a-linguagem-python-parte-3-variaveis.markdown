---
layout: post
title:  "Introdução a linguagem python parte 3 - Tipos de Variável"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Variável e tipos de dados no Python

Variáveis são um dos recursos mais básicos das linguagens de programação. As variáveis são utilizadas para armazenar valores em memória (i.e., no seu computador), elas nos permitem gravar e ler esses dados com facilidade a partir de um nome definido por nós.

Tipos de variaveis no python:
* números com valores __inteiros__ (e.g., 1, 2, 50, 199 etc...),
* números com valores __flutuantes__ (e.g., 1.1, 2.5, 50.02, 199.001 etc...),
* letras, palavras ou textos inteiros conhecidos como __strings__ (e.g., "Rafael Sanches", 'Azul', 'Qualquer texto' etc...)
* valores __booleanos__ (i.e., Falso ou Verdadeiro). Dentro desse contexto os valores númericos 0 pode ser considerado como falso e 1 como verdadeiro,
* __variáveis heterogêneas__ como __listas__, __dicionários__, __tuplas__, __sets__, __arrays__ e __matrizes__ que serão apresentadas em outra momento no decorrer desse post.

O tipo de variável número complexo por eu nunca ter precisado utilizar na minha jornada de desenvolvedor não será apresentado nesse post. Para maiores interessados(as) do que é um número complexo e afins segue [link](https://pt.wikipedia.org/wiki/N%C3%BAmero_complexo#:~:text=representa%20o%20n%C3%BAmero%20Z%20em,parte%20real%20da%20parte%20imagin%C3%A1ria.&text=e%20o%20semi%2Deixo%20real,complexo%20Z%20e%20denotado%20por).

Para criar uma variável no python é bastante simples, basta informar o nome da variável seguida do operador de atribuição (i.e., __=__ ) e na sequência o valor que será inserido nessa variável. Veja no exemplo a seguir para ficar mais claro:

```python
# String
nome = 'Rafael Sanches'

# Inteiro
num1 = 1

# Flutuante
num2 = 1.5

# Boleano
status = True

# Lista
compras = ['leite', 'queijo', 'pão']

# Dicionário
cliente = {'nome':'Rafael Sanches','idade':28,'sexo':'M','cargo':'Analista de Dados','aniversario':'04-10-1991'}

# Tupla é uma Lista imutável. O que diferencia a Estrutura de Dados Lista da Estrutura de Dados Tupla é que a primeira pode ter elementos adicionados a qualquer momento, enquanto que a segunda estrutura, após definida, não permite a adição ou remoção de elementos.
dados_inalteraveis = ("x", "y", 10, 20, "c")

# Array e Matrizes
# Em python um array nada mais é do que uma lista simples com tamanho predefinido
# Em python uma matriz nada mais é do que uma lista de listas com tamanhos predefinidos
# Exemplos:

# array com 4 posições
array = [1, 2, 3, 4]

# matriz de 2 linhas e 3 colunas
matriz = [
[1, 2, 3],
[1, 2, 3]
]

# Sets (conjuntos que não permitem valores duplicados)
conjunto_a = set([1, 2, 3, 4])

```

Para deixar as coisas por aqui mais interessantes, vamos colocar a mão na massa para entender mais sobre variáveis.

Para usar o python 3 no linux digite no terminal:
```
python3
```
Nos demais sistemas operacionais isso não é necessário caso você tenha apenas a versão 3 do python instalado no seu sistema operacional então, nesse caso basta digitar somente:
```
python
```

Se tudo ocorreu bem, você deve ver algo no seu terminal semelhante a isso:
```bash
Python 3.6.8 (default, Jan 14 2019, 11:02:34)
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
Ao atribuir um valor a uma variável no terminal, digite o nome da variável e aperte a tecla __ENTER__ para visualizar o conteúdo da variável no seu terminal.

Exercícios para praticar o que aprendeu:

1. Criar uma variável chamada nome e atribuir o seu nome a ela.

2. Criar uma variável chamada idade e atribuir a sua idade a ela.

3. Criar uma variável chamada camiseta e atribuir um valor flutuante (i.e., valor quebrado) a ela.

4. Criar uma variável chamada felicidade e atribuir um valor booleano a ela.

5. Criar uma variável chamada amigos e atribuir cinco nomes de amigos utilizando listas a ela.

6. Criar uma variável chamada funcionário e atribuir um dicionário a ela com suas informações tais como: nome, idade, email e telefone.
