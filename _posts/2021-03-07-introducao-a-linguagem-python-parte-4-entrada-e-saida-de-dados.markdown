---
layout: post
title:  "Introdução a linguagem python parte 4 - Entrada e Saída de Dados"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Entrada e Saída de Dados

A entrada de dados refere-se a entrada de dados do mundo externo para o meio digital (e.g., de você para o seu computador, celular ou tablet). É dessa forma que enviamos informações para dentro das nossas aplicações. A saída de dados por outro lado refere-se a apresentação dos dados armazenados para o usuário.

No python a entrada de dados funciona por meio da função __input__.  Apartir da versão 3 do python, a função __input()__, tem por objetivo informar um texto para o usuário e em seguida, ativar o modo de digitação, isto é, colocar o seu __terminal__  de uma determinada forma em que seja possível a digitação (entrada de dados). A seguir um exemplo da utilização dessa função.

```bash
>>> nome = input("Qual seu nome?\n")
Qual seu nome?
Rafael
>>> nome
'Rafael'

```
No código acima, a variável __nome__ vai receber o conteúdo que o usuário informar pelo terminal. Outro detalhe a se observar é o __\n__ ele no final da string significa que o terminal deve pular uma linha para você de acordo com sua posição na string\mensagem. Vale ressaltar também que toda informação vinda deste modo é atribuida como texto a variável nome independente se o usuário digitar um número qualquer. Nesse caso, se você deseja informar um dado do tipo numérico você deve fazer o seguinte.

```bash
>>> inteiro = int(input("informe um numero de 1 a 10: \n"))
informe um numero de 1 a 10:
5
>>> inteiro
5
>>> type(inteiro)
<class 'int'>

>>> flutuante = float(input("informe um numero de 1.0 a 10.0: \n"))
informe um numero de 1.0 a 10.0:
1.7
>>> flutuante
1.7
>>> type(flutuante)
<class 'float'>

```
No código acima estamos adicionando as funções __int()__ e __float()__ que servem para transformar o conteúdo digitado pelo usuário nos seus respectivos tipos. Outra função que utilizei agora foi a função __type()__ essa função tem por natureza retorna o tipo da variável que você passar a ela por parâmetro.

A seguir vou apresentar exemplos de saída de dados e para isso vou utilizar a função __print()__ e depois vou explicando o que foi feito.

```bash
>>> nome = input("Informe seu nome:\n")
Informe seu nome:
Rafael
>>> print("O nome informado foi: ",nome)
O nome informado foi:  Rafael
>>> print("O nome informado foi: {} ".format(nome))
O nome informado foi: Rafael
>>>
```

Como é possível observador no exemplo acima eu apresentei duas formas de apresentar seu dado utilizando a função print. No primeiro exemplo eu apenas mesclo o texto a ser exibido com a variável separando o texto por meio de virgula (",") e na sequência a respectiva variável que ira conter o conteúdo a ser exibido naquela parte do texto.

O outro exemplo tem a mesma finalidade mas, você não precisa ficar mesclando seu texto com variáveis e virgulas e ele deixa sua mensagem mais limpa e elegante. Nesse exemplo nos adicionamos a função __format()__ essa é uma função utilizada com dados do tipo __string__. Ela funciona da seguinte forma, você escreve seu texto/mensagem e nela no local onde você deseja que suas variáveis apareçam você utiliza __{}__ no final da sua __string__ você coloca "." e digita __format()__ como parâmetro na função format você passa as suas respectivas variáveis separadas por virgula na sequência que você deseja que elas apareçam na sua mensagem e no caso as variáveis vão assumir os __{}__.

Exercícios para praticar o que aprendeu:

1. Criar uma variável chamada nome e outra chamada sobrenome e atribuir o seu nome e sobrenome a cada uma delas, faça isso utilizando a função que aprendeu para entrada de dados e depois gerar uma saída indicando o nome e sobre utilizando a função para apresentar dados.

2. Criar uma variável chamada nome e outra chamada sobrenome e atribuir o seu nome e sobrenome a cada uma delas, faça isso utilizando a função que aprendeu para entrada de dados e depois gerar uma saída indicando o nome e sobre utilizando a função para apresentar dados. Nesse exemplo utilize a função __format__ para formatar sua mensagem e altere a sua mensagem para algum conteúdo diferente do acima do jeito que desejar.

3. Faça um programa que solicite dois número ao usuário do computador e apresente a soma deles. Faça o mesmo para subtração, multiplicação e divisão. Obs: não se esqueça de __converter__ os valores informados.  
