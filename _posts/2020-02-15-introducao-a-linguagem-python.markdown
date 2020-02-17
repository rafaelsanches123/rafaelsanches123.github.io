---
layout: post
title:  "Introdução a linguagem python"
date:   2020-02-15 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre a linguagem de programação __python__. No post de hoje eu vou compartilhar com vocês conceitos básicos de programação com a lingaugem python de modo que, eu possa ajudá-los a utilizar esse recurso fantástico na sua vida. Com essa linguagem você pode resolver problemas do mundo digital dos mais diversos,  sendo eles: matemáticos, estatísticos, web (i.e., na internet), desktop (i.e., no seu computador), para dispositivos moveís (i.e., no seu celular pessoal) e mais uma infinidade de problemas. No momento atual, estamos vivendo um __hype__ com essa linguagem devido a popularidade do mundo __Big Data__, __Machine Learning__, __Mineração de Dados__ e __Data Science__.

A seguir, vou falar um pouco da história dessa linguagem, como instalar e configurar ela na sua máquina e na sequência vou introduzir os conceitos de variável, operadores lógicos, estruturas condicionais, laços de repetição, estruturas de dados do python (i.e., listas, dicionários, tuplas, ideia de vetores e matrizes no python), funções e módulos. Em cada uma dessas etapas vou apresentar a vocês desafios para que você possa treinar tudo aquilo que for ensinado em cada parte dessa aula preparada para você que é ou não familiarizado com o mundo digital.

## História do python

Python é uma linguagem de programação de alto nível, interpretada, de __script__, imperativa, orientada a objetos, funcional e de tipagem dinâmica. Foi criada por __Guido Van Rossum__ em 1991. Atualmente possui um modelo de desenvolvimento __comunitário__, aberto e gerenciado pela organização sem fins lucrativos __Python Software Foundation__.

A linguagem foi projetada com a filosofia de enfatizar a importância do esforço do programador sobre o esforço computacional. Prioriza a __legibilidade do código__ sobre a __velocidade__ ou expressividade. Combina uma __sintaxe concisa__ e __clara__ com os recursos poderosos de sua biblioteca padrão e por módulos e frameworks desenvolvidos por terceiros.

Python é uma linguagem de __propósito geral__ de alto nível, multiparadigma, suporta o paradigma orientado a objetos, imperativo, funcional e procedural. Possui tipagem dinâmica e uma de suas principais características é permitir a __fácil leitura do código__ e exigir __poucas linhas de código__ se comparado ao mesmo programa em outras linguagens. Devido às suas características, ela é utilizada em diferentes problemas. Foi considerada pelo público a 3ª linguagem "mais amada", de acordo com uma pesquisa conduzida pelo site [Stack Overflow](https://insights.stackoverflow.com/survey/2018#technology) em 2018, e está entre as 5 linguagens mais populares, de acordo com uma pesquisa conduzida pela [RedMonk](https://redmonk.com/sogrady/2018/03/07/language-rankings-1-18/).

O nome Python teve a sua origem no grupo humorístico britânico __Monty Python__, embora muitas pessoas façam associação com o réptil do mesmo nome.

## Instalando e configurando o python no seu computador

### Windows

Uma das formas mais simples de instalar o python, pode ser utilizando o ananconda que é um gerenciador de pacotes que já vem preparado com algumas bibliotecas do python ou somente o python de forma mais crú direto do site do python. Para usar o anaconda, basta acessar o site do [Anaconda](https://docs.anaconda.com/anaconda/install/windows/), baixar o arquivo executável de instalação referente ao seu sistema operacional windows (64bit ou 32bit) e clicar 2x no arquivo executável e ir clicando em próximo até finalizar o processo de instalação. Antes de finalizar o processo de instalação, se aparecer uma opção com checkbox para assinalar e conter a informação se você deseja vincular a sua instalação python a variavel __PATH__ de ambiente do windows pode marcar essa opção pois, isso te permitirá utilizar o python dentro do CMD do windows.

Se tiver alguma dúvida, apenas vá clicando em próximo sem se preocupar e sem medo de algo dar errado.

O processo acima também é válido para instalação somente do python sem bibliotecas adicionais. Para isso basta acessar o site do [Python](https://www.python.org/downloads/windows/) e fazer o mesmo processo supracitado.

### Linux

Ubuntu 17.10, Ubuntu 18.04 e versões acima  já vem com Python 3.6 por padrão. Para invocar o python no seu computador, basta abrir o terminal e digitar os comandos a seguir de acordo com a versão que deseja utilizar:

Para utilizar o python na sua versão 2 digite no terminal:
```
python
```
Para utilizar o python na sua versão 3 que é a mais atual digite no terminal:
```
python3
```

Ubuntu 16.10 and 17.04 não vem com o Python 3 por padrão mas, ele está no repositório universal do Ubuntu. Para instalá-lo abra seu terminal de linha de comando e digite o comando a seguir:
```
sudo apt-get update
sudo apt-get install python3.6
```

### MacOS

Primeira coisa a se fazer é instalar o gerenciador de pacotes do MacOs o HomeBrew. Para isso acesse o site com todos os passos para isso [HomeBrew](https://brew.sh/). Depois de instalar o HomeBrew, basta abrir um terminal e digitar o comando a seguir:
```
brew install python3
```

## Variável e tipos de dados no Python

Variáveis são um dos recursos mais básicos das linguagens de programação. As variáveis são utilizadas para armazenar valores em memória (i.e., no seu computador), elas nos permitem gravar e ler esses dados com facilidade a partir de um nome definido por nós.

Tipos de variaveis no python:
* números com valores __inteiros__ (e.g., 1, 2, 50, 199 etc...),
* números com valores __flutuantes__ (e.g., 1.1, 2.5, 50.02, 199.001 etc...),
* letras, palavras ou textos inteiros conhecidos como __strings__ (e.g., "Rafael Sanches", 'Azul', 'Qualquer texto' etc...)
* valores __booleanos__ (i.e., Falso ou Verdadeiro). Dentro desse contexto os valores númericos 0 pode ser considerado como falso e 1 como verdadeiro,
* __variáveis heterogêneas__ como __listas__, __dicionários__, __tuplas__, __sets__, __arrays__ e __matrizes__ que serão apresentadas em outra momento no decorrer desse post.

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

2. Criar uma variável chama idade e atribuir a sua idade a ela.

3. Criar uma variável chamada camiseta e atribuir um valor flutuante (i.e., valor quebrado) a ela.

4. Criar uma variável chamada felicidade e atribuir um valor booleano a ela.

5. Criar uma variável chamada amigos e atribuir cinco nomes de amigos utilizando listas a ela.

6. Criar uma variável chamada funcionário e atribuir um dicionário a ela com suas informações tais como: nome, idade, email e telefone.

## Operadores Lógicos, Aritméticos e Relacionais

Operadores Lógicos:
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
Operadores Aritméticos:
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

Operador Relacional:
É todo operador que obtém a relação do membro a esquerda com o membro a sua direita. Na tabela abaixo, temos os operadores relacionais disponibilizados pelo python.

Descrição |	Operador
:------:|:------:
Maior que |	>
Menor que |	<
Igual a | ==
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

>>> 10 >= 2
True

>>> 10 <= 2
False

```

Exercícios para praticar o que aprendeu:

1. Criar uma variável e chamada de __maior_valor__ e atribuir a ela o valor 10. Criar uma variável e chamada de __menor_valor__ e atribuir a ela o valor 3.

2. Usando o operador de __igual a__ verificar se o valor de __maior_valor__ é igual ao conteúdo da variável __menor_valor__.

3. Usando o operador __maior que__ verificar se o valor de __maior_valor__ é maior que o conteúdo da variável __menor_valor__.

4. Usando o operador __menor que__ verificar se o valor de __maior_valor__ é menor que o conteúdo da variável __menor_valor__.

Em construção...


## Estruturas condicionais

Em construção...

## Laços de repetição

Em construção...

## Estruturas de dados

Em construção...

## Funções

Em construção...

## Módulos

Em construção...
