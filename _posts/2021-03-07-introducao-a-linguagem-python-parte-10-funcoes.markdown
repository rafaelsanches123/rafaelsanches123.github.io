---
layout: post
title:  "Introdução a linguagem python parte 10 - Funções"
date:   2021-03-06 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Funções

Funções são uma das ferramentas mais poderosas quando falamos de programação de computadores. As funções fornecem ao programador(a) o poder de __reuzar um pedaço de código__ em __mais de um local diferente__ do seu código/projeto. Saber usar funções é fundamental também para que você tenha um código mais limpo e organizado de modo que você consiga fazer a __manutenção__ do mesmo de __forma mais suave__ quando necessário.

A primeira coisa que vem a minha cabeça quando eu escuto a o termo __"função"__ é uma frase que uma professora que me deu aula na graduação falava para minha turma que era __"Dividir para conquistar"__ e essa frase faz todo o sentido depois que você entendo como trabalhar com funções independente da linguagem de programação que você esteja utilizando.

Como criar uma função no python? Como é a sua sintaxe?
```python

def nome_da_funcao(param1, param2, param3):
  resultado = param1 + param2 + param3
  return resultado

def nome_da_funcao(param1, param2, param3):
  resultado = param1 + param2 + param3
  print("Resultado da Função: {}".format(resultado))

def nome_da_funcao(param1, param2, param3):
  param1 = param1 + 5
  param2 = param2 + 3
  param3 = param3 + 7
  return param1, param2, param3

```
Pontos importantes:
* Toda função em python começa com a palavra reservada __def__;
* __def__ é sempre precedida do nome da função como por exemplo: __nome_da_funcao__ sem caracteres especiais;
* __nome_da_funcao__ por sua vez é precedida de __(__ __)__ onde, dentro dos parenteses serão passados os parâmetros para sua função. Esses parâmetros podem ser valores que você irá modificar para retornar pos alteração por exemplo;
* Sua função pode retornar um valor único;
* Sua função pode retornar multiplos valores/variáveis;
* Sua função pode não retornar nada também.

Bora lá devs, entender melhor sobre funções. A seguir vou lhes apresentar um caso muito simples de se utilizar funções. Vamos imaginar uma calculadora que tenha 4 funcionalidades: __Somar__, __Subtrair__, __Multiplicar__ e __Dividir__.

Abra o seu terminal e borá colocar a mão na massa:

```bash

>>> def somar(num1, num2):
...   return num1 + num2
...
>>> def subtrair(num1, num2):
...   return num1 - num2
...
>>> def multiplicar(num1, num2):
...   return num1 * num2
...
>>> def dividir(num1, num2):
...   return num1 / num2
...
>>> resultado = somar(10,5)
>>> resultado
15
>>> resultado = subtrair(10,5)
>>> resultado
5
>>> resultado = multiplicar(10,5)
>>> resultado
50
>>> resultado = dividir(10,5)
>>> resultado
2.0
```

Nos exemplos acima, foram criadas __4 funções__ uma para somar 2 números, subtrair, multiplicar e dividir. Assim como apresentados os pontos importantes é interessante observar que nossa códificação segue exatamente o que foi descrito no começo e também é possível observar que trabalhar com funções é algo bastante simples em python.

Depois de ver o exemplo acima, acredito que você meu caro(a) leitor(a) você está pronto para praticar e entender mais sobre funções.

Exercícios para praticar o que aprendeu:

1. Crie um programa semelhante a uma calculadora:
* Primeiro Solicite um número inteiro entre 1 e 4.
* Se o usuário digitar 1 você deve solicitar 2 novos números para ele e realizar a ação de somar esses 2 novos números;
* Se o usuário digitar 2 você deve solicitar 2 novos números para ele e realizar a ação de subtrair esses 2 novos números;
* Se o usuário digitar 3 você deve solicitar 2 novos números para ele e realizar a ação de multiplicar esses 2 novos números;
* Se o usuário digitar 4 você deve solicitar 2 novos números para ele e realizar a ação de dividir esses 2 novos números;
* Para sair do laço de repetição solicite ao usuário que informe um número -1.

2. Crie um programa que leia um número e imprima na tela do computador se ele é Par ou Ímpar.

3. Crie um programa que leia um número e imprima se esse número é palindromo ou não. Obs: um número palindromo é aquele que siginifica a mesma coisa de trás para frente ex: 121.

4. Crie um programa que receba uma lista de números e retorne o menor número da lista.

5. Crie um programa que receba uma lista de números e retorne o maior número da lista.

6. Crie um programa que receba uma lista de números e calcule a soma desses números da lista.

7. Crie um programa que leia uma lista e retorno a sua versão reversa.
