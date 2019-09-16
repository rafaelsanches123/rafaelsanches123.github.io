---
layout: post
title:  "Introdução a linguagem python"
date:   2019-08-10 10:10:03 -0300
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

## Variável

Variáveis são um dos recursos mais básicos das linguagens de programação. As variáveis são utilizadas para armazenar valores em memória (i.e., no seu computador), elas nos permitem gravar e ler esses dados com facilidade a partir de um nome definido por nós.

Tipos de variaveis no python:
* números com valores __inteiros__ (e.g., 1, 2, 50, 199 etc...),
* números com valores __flutuantes__ (e.g., 1.1, 2.5, 50.02, 199.001 etc...),
* letras, palavras ou textos inteiros conhecidos como __strings__ (e.g., 'Rafael Sanches', 'Azul', 'Qualquer texto' etc...)
* valores __booleanos__ (i.e., Falso ou Verdadeiro). Dentro desse contexto os valores númericos 0 pode ser considerado como falso e 1 como verdadeiro,
* __variáveis heterogêneas__ como __listas__, __dicionários__, __tuplas__, __arrays__ e __matrizes__ que serão apresentadas em outra momento no decorrer desse post.

Para criar uma variável no python é bastante simples, basta informar o nome da variável seguida do operador de atribuição (i.e., __=__ ) e na sequência o valor que será inserido nessa variável. Veja no exemplo a seguir para ficar mais claro:

```
nome = 'Rafael Sanches'
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
```
Python 3.6.8 (default, Jan 14 2019, 11:02:34)
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

## Operadores Lógicos

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
