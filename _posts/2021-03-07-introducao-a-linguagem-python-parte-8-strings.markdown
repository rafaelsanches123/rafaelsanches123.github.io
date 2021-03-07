---
layout: post
title:  "Introdução a linguagem python parte 8 - Strings"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Strings

No python uma string é um tipo de várivel que contém uma sequência de caracteres ou números (Observação: Lembre-se que se você informar um número como string ele não é do tipo inteiro e nem flutuante nesse caso). Uma string sempre é circundada por aspas duplas ou apostofre dupla também. Exemplo: "Texto de exemplo" ou 'Texto de exemplo' repare que ambos seguem a regra dita anteriormente.

Abra o seu terminal e faça o mesmo apresentado a seguir:

```bash

>>> string = "Exemplo de texto"
>>> print(string)
Exemplo de texto
>>> string1 = '1'
>>> print(string1)
1
>>> string2 = "1.2"
>>> print(string2)
1.2

>>> print(type(string))
<class 'str'>
>>> print(type(string1))
<class 'str'>
>>> print(type(string2))
<class 'str'>

```

No exemplo acima é possível observar que mesmo para números, sejam eles inteiros ou flutuantes, se estiverem no modelo do tipo string eles não são utilizados mais como números e sim como textos. Um exemplo disso ocorre se você tentar realizar alguma operação matemática com eles veja o exemplo a seguir:

imagine que você tenha 2 variáveis:

```bash

>>> num1 = "10"
>>> num2 = "5"

```
Se você tentar realizar as operações básicas de subtração, multiplicação e divisão você irá obter um erro avisando que esse tipo de tarefa não é possível de ser feito pois você está utilizando variáveis do tipo string. Se você tentar realizar a operação de adição ela não vai gerar um erro de compilação e para seu código mas, se você tentar somar essa duas varáveis você irá obter o seguinte:


```bash

>>> num1 = "10"
>>> num2 = "5"
>>> res = num1 + num2
>>> print(res)
105
```

Ué, mas o que aconteceu? Então, isso aconteceu porque no python quando você utiliza o operador de soma __+__ com strings ele realiza a junção dessas duas string e as transforma em apenas 1. Acredito que foi simples entender o que aconteceu não foi mesmo?

A seguir, vou apresentar algumas funções disponiveis no python para trabalharmos com string e que podem ajudar muito sua vida na criação de algum programa que necessite o uso de strings.

Como saber o tamanho de uma string?
Para saber o tamanho de uma string, basta utilizar a função __len()__. Essa função retorna um valor inteiro referente a quantidade de caracteres presentes em uma string veja alguns exemplos a seguir:

```bash
>>> string1 = "Rafael"
>>> len(string1)
6
>>> print("A string1 tem o tamanho: ",len(string1))
A string1 tem o tamanho:  6

>>> string2 = "Eu sou programador(a)!"
>>> len(string2)
22

```

Observação: lembre-se que o espaço em branco entre caracteres também é computado como uma posição na string. Por esse motivo a string2 tem o tamanho 22 e não 20.

Muito simples não é mesmo!

Agora vou relembrar a você meu caro(a) leitor(a) uma função muito bacanuda que nós conhecemos no início do post chamada __format()__. Ela é bastante simples e também nos permite inserir valores em posições desejadas em uma string por meio de __{}__ dentro da string. A seguir eu vou apresentar o modelo visto no início do post e um plus dessa função de modo que você consiga alterar a posição dos elementos inseridos na string.

```bash
>>> string = "O número {} é maior que o número {} e meu nome é {}".format(10, 2, "Rafael")
>>> print(string)
O número 10 é maior que o número 2 e meu nome é Rafael
>>> string = "O número {1} é maior que o número {2} e meu nome é {0}".format(10, 2, "Rafael")
>>> print(string)
O número 2 é maior que o número Rafael e meu nome é 10
```

No código acima perceba que na primeira utilização do método __format__ dentro dele, você passa como parâmetro os conteudos/variáveis respectivos(as) dos pares de chaves seguindo a ordem de precedência que eles aparecem como parâmetros na função format. No segundo caso um plus não mencionado sobre esse método no ínicio do post é que se você enumerar o interior do par de chaves com um número que esteja dentro da quantidade de parâmetros na função format a variável/conteúdo daquela posição irá ser movido para esse respectivo par de chaves. Vale ressaltar também que a primeira posição de chaves começa sempre por zero e não por 1 e isso pode acabar confundindo sua cabeça na hora de realizar isso. Uma boa prática nesse caso seria deixar as chaves sem númeração e colocar os parâmetros da função format na ordem que eles devem aparecer na string.

Como acessar o conteúdo de uma posição especifica na string?
Muito simples, basta utilizar colchetes na frente da sua string ou variável que contem sua string e acessar a posição desejada. Segue um exemplo:

```bash

>>> "python"[0] # 'p'
'p'
>>> "python"[1] # 'y'
'y'
>>> "python"[2] # 't'
't'
>>> "python"[3] # 'h'
'h'
>>> "python"[4] # 'o'
'o'
>>> "python"[5] # 'n'
'n'
>>> string = "Rafael"
>>> string[0]
'R'
>>> string[7]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range

```

No exemplo acima são ilustrados 3 casos: 1º acessando a posição do conteúdo diretamente da string, 2º atribuindo a string a uma variável e acessando a posição desejada na sequência e 3º quando você tentar acessar uma posição que não exista na string você receberá como feedback do python a mensagem explicitando que você tentou acessar uma posição fora dos limites ou do tamanho da sua string.

Uma observação sobre strings: não podemos alterar seu valor atribuindo um valor através do índice. Como no exemplo a seguir:

```bash

>>> string = "Rafael"
>>> string[0] = "A"
Traceback (most recent call last):
  File "main.py", line 2, in <module>
    string[0] = "A"
TypeError: 'str' object does not support item assignment
```

A forma mais comum de se substituir alguma coisa dentro de uma string é utilizando a função __replace()__. No código a seguir, vamos definir uma string e em seguida, substituir uma parte do seu conteúdo por outra.

```bash
>>> texto = "A função replace aaaaaa substitui parte de um texto por outro texto"
>>> texto.replace("aaaaaa", "basicamente")
'A função replace basicamente substitui parte de um texto por outro texto'
>>>
```

No código acima foi definido uma variável do tipo string chamada texto e dentro desta nós colocamos uma marcação __aaaaaa__, somente para facilitar o entendimento da função __replace__. Em seguida, invocamos a funçao replace(), e dissemos, que queríamos alterar a string __aaaaaa__ pelo conteúdo, __"basicamente"__. Feito isso, uma nova string foi retornada com a alteração realizada.

Novamente é importante relembrar que o que foi retornado é uma nova string, até porque, a string utilizada não pode ser alterada assim como já expliquei antes.

Vale ressaltar que o tipo string é um objeto iterável então podemos andar pelas posições da string utilizando um laço de repetição. Veja um exemplo a seguir:

```bash
>>> for letra in string:
...   print(letra)
...
R
a
f
a
e
l
>>> for indice,letra in enumerate("Rafael"):
...   texto = "Posicao: {}, Letra: {}".format(indice, letra)
...   print(texto)
...
Posicao: 0, Letra: R
Posicao: 1, Letra: a
Posicao: 2, Letra: f
Posicao: 3, Letra: a
Posicao: 4, Letra: e
Posicao: 5, Letra: l
```

Outra coisa super bacana que podemos fazer com strings é recuperar uma parte da string (i.e., fatiar a string que em inglês você verá esse conceito como "slice"). Fazer isso é algo bastante simples, vejamos alguns exemplos a seguir:

```bash
>>> string = "Rafael"
>>> string
'Rafael'
>>> string[1:4]
'afa'
>>> string[0:3]
'Raf'
>>> string[:3]
'Raf'
>>> string[-1]
'l'
>>> string[-2]
'e'
>>> string[:]
'Rafael'
>>> string[0:]
'Rafael'
```

Se eu quiser deixar minha string com todo o contéudo em __caixa alta__ (i.e., em letra maiuscúla) eu preciso utilizar o método __upper()__. Veja um exemplo a seguir:

```bash
>>> string = "Meu nome é Rafael!"
>>> string
'Meu nome é Rafael!'
>>> string.upper()
'MEU NOME É RAFAEL!'
```

Se eu quiser deixar minha string com todo o contéudo em __caixa baixa__ (i.e., em letra minuscúla) eu preciso utilizar o método __lower()__. Veja um exemplo a seguir:

```bash
>>> string = "MEU NOME É RAFAEL!"
>>> string
'MEU NOME É RAFAEL!'
>>> string.lower()
'meu nome é rafael!'
```

Se eu quiser converter uma variável númerica em string eu preciso utilizar o método __str()__. Veja um exemplo a seguir:

```bash
>>> numero = 10
>>> numero
10
>>> type(numero)
<class 'int'>
>>> str(numero)
'10'
>>> type(str(numero))
<class 'str'>
```

Se eu precisar descobrir se existe ou não apenas letras na minha string eu preciso utilizar o método __isalpha__. Veja um exemplo a seguir:

```bash
>>> "Rafael".isalpha()
True
>>> "Rafa1l".isalpha()
False
>>> "123".isalpha()
False
```

Se eu precisar remover espaços vazios ao redor da string eu preciso utilizar o método __strip__. Veja um exemplo a seguir:

```bash
>>> " sobrando espaços ".strip()
'sobrando espaços'
>>> "  sobrando espaços   ".strip()
'sobrando espaços'
```

Se eu precisar juntar cada item de uma string por meio de um delimitador específico eu preciso utilizar o método __join()__. Veja alguns exemplos a seguir:

```bash
>>> string ="Eu estou com calor by Renata!"
>>> string
'Eu estou com calor by Renata!'
>>> "_".join(string)
'E_u_ _e_s_t_o_u_ _c_o_m_ _c_a_l_o_r_ _b_y_ _R_e_n_a_t_a_!'
>>> "-".join(['Rafael','Programacao','Blog'])
'Rafael-Programacao-Blog'
>>> " ".join(['Rafael','Programacao','Blog'])
'Rafael Programacao Blog'
```

Nos exemplos acima, eu também ilustrei que é possível juntar listas que é uma estrutura de dados utilizada em python e que será melhor detalhada no próximo tópico.

E se eu não gostei do que eu juntei e também se eu pegar alguma string que eu queira separar os itens o que eu devo utilizar? Nesse caso, você precisa utilizar o método __split()__. Veja alguns exemplos a seguir:


Repare que o método __split()__ também utiliza um delimitador para separar a string diferente do método __join()__ que usa um delimitador para juntar os itens da string. O __split()__ é o inverso do método __join()__. Veja alguns exemplos a seguir:

```bash
string = "nome - sobrenome"
>>> string.split("-")
['nome ', ' sobrenome']
>>> string = "1,2,3,4,5,6"
>>> string.split(" ")
['1,2,3,4,5,6']
>>> string.split(",")
['1', '2', '3', '4', '5', '6']
```

Esses foram apenas alguns métodos que você pode aplicar para trabalhar com strings, se quiser conhecer outros não mencionados aqui, eu recomendo que você acesse a documentação do python e explore ainda mais esse universo.

Exercícios para praticar o que aprendeu:

1. Criar uma variável do tipo string e atribuir o seu nome a ela. Depois de atribuir seu nome a variável criada, imprima seu conteúdo na tela com a seguinte frase: "Olá eu sou: " e imprima o seu nome após os ":".

2. Criar uma variável e atribuir seu nome a ela. Criar uma segunda variável e atribuir o nome de uma pessoa que você gosta a ela. No final imprimir o resultado da concatenação do conteúdo da primeira variável "+" a seguinte frase " curte " "+" com o conteúdo da segunda variável que você criou. Exemplo de resultado: "Rafael curte Renata".

3. Criar uma variável e atribuir seu nome completo a ela. Depois de atribuir seu nome completo a ela imprimir a quantidade de caracteres que tem no seu nome completo. Dica: lembre de antes de apresentar o valor subtrair com a quantidade de espaços vazios entre as palavras.

4. Criar uma variável e atribuir o nome do seu animal de estimação a ela. Depois de atribuir o nome do seu pet a variável, criar uma frase e adicionar a variável na frase utilizando a função __format()__.

5. Criar uma variável e atribuir o seguinte texto a ela "O rato roeu a roupa do rei de Roma". Depois de atribuir o texto a variável, imprimir o conteúdo do texto substituindo a palavra "rei" pelo seu nome.

6. Criar uma variável e atribuir o seu nome completo a ela. Depois de atribuir o seu nome completo a variável, imprimir somente as 3 primeiras letras do seu nome.

7. Criar uma variável e atribuir o conteúdo "Eu sou grande!" o a ela. Depois de atribuir o conteúdo a variável, imprimir todo o conteúdo em caixa alta.

8. Criar uma variável e atribuir o conteúdo "Eu sou pequeno!" o a ela. Depois de atribuir o conteúdo a variável, imprimir todo o conteúdo em caixa baixa.

9. Faça um programa que solicite ao usuário 2 variáveis onde, a primeira recebera um texto e a segunda um outro texto com conteúdo diferentes. Verifique qual variável tem o tamanho maior entre as duas e imprimir qual é a maior.

10. Faça um programa que solicite um texto e separe ele por meio do delimitador "*".
