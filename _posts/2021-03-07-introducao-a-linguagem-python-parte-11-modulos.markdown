---
layout: post
title:  "Introdução a linguagem python parte 11 - Módulos"
date:   2021-03-06 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Módulos

Os módulos em python é um conceito relacionado a capacidade de importar funções para você utilizar em outro código. Ué, como assim? Bom, vou explicar melhor. Aqui diferente dos demais tópicos estudados anteriormente, você irá precisar criar pelo menos dois arquivos com a extensão __.py__ para entender o conceito de módulo.

Primeiro vamos criar um arquivo com seu editor de texto favorito e chamar ele de __main.py__ e criar um segundo arquivo chamado __calculadora.py__ ok?

vamos começar com o conteúdo do arquivo __calculadora.py__. O arquivo __calculadora.py__ irá conter o seguinte código:

```python

def somar(num1, num2):
  return num1 + num2

def subtrair(num1, num2):
  return num1 - num2

def multiplicar(num1, num2):
  return num1 * num2

def dividir(num1, num2):
  return num1 / num2

```

Agora, o conteúdo do arquivo __main.py__ será:


```python

import calculadora

num1 = 20
num2 = 3

resultado = calculadora.somar(num1, num2)
print("{} + {} = {}".format(num1, num2, resultado))

resultado = calculadora.subtrair(num1, num2)
print("{} - {} = {}".format(num1, num2, resultado))

resultado = calculadora.multiplicar(num1, num2)
print("{} x {} = {}".format(num1, num2, resultado))

resultado = calculadora.dividir(num1, num2)
print("{} / {} = {}".format(num1, num2, resultado))

```

Quando você executar o código acima irá obter o seguinte resultado:

```bash

20 + 3 = 23
20 - 3 = 17
20 x 3 = 60
20 / 3 = 6.666666666666667


```

Utilizar módulos é muito bom para que você possa organizar suas funções de acordo com algum objetivo. E seu uso é bastante simples como foi ilustrado acima. Você simplesmente cria um arquivo com as funções que pretende utilizar. Cria outro arquivo que irá utilizar suas funções e por meio da palavra reservada __import__ você menciona o módulo/nome do seu script python e a partir dessa chamada você consegue acessar as funções que criou dentro desse módulo python.

O exemplo acima foi tão simples e ilustrativo que eu acredito que não seja necessário mais exemplos para ilustrar seu conceito.
