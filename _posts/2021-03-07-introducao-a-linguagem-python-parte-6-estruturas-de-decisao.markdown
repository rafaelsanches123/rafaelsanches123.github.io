---
layout: post
title:  "Introdução a linguagem python parte 6 - Estruturas de Decisão"
date:   2021-03-04 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Estruturas de Decisão

Durante o fluxo de algum raciocínio humano ocorre-se a necessidade de tomar uma decisão se, certa condição ocorrer e de tomar outra decisão se, alguma outra coisa ocorrer. Na linguagem python quando você tem essas mesmas necessidades costuma-se utilizar a palavras reservadas __if__ e __else__ dependendo do que se deseja alcançar e também a casos em que você queira ter mais de uma condição seguida dependendo que deseja analisar.

Para deixar isso mais claro vamos ver como isso ocorre na prática:

Imagine a seguinte situação: você é uma caixa de supermercado e uma pessoa compra um produto que custa 35,00 reais e ela te dá 55,00 reais __Se__ o valor pago for __maior que__ o valor de custo do produto, você terá que fornecer troco correto? Isso mesmo, esse é um exemplo simples de condição.

Passando isso para um problema computacional teremos o seguinte, abra seu terminal e faça:

```bash
>>> produto = 33.00
>>> produto
33.0
>>> pago = 55.00
>>> pago
55.0
>>> pago - produto
22.0
>>> if( produto < pago ):
...     print('seu cliente precisa de troco!')
...
precisa de troco!
>>>

```

Acima podemos ver 2 comandos novos a estrutura de condição simples __if__ que nos ajuda a analisar uma expressão e se essa expressão resulta em verdade ela será realizada se não, não acontecerá nada no caso acima é claro. Ainda no exemplo acima foi possível observar o comando __print__. O comando print ele tem a função de imprimir algo na tela do seu computador (i.e., saída de dados) seja um texto simples, composto ou mesmo o conteúdo de alguma variável. Não se preocupe pois, vamos utilizar ele bastante no decorrer desse post para visualizar nossas ações ou apresentar respostas na tela do computador.

Existem certas ocasiões que se algo não acontecer outra decisão precisa ser tomada. Seguindo ainda o mesmo exemplo do troco imagine que agora o cliente pagou o valor exato do produto no caixa e ele não vai precisar receber troco nesse caso podemos expressar isso utilizando estruturas de decisão utilizando a palavra reserva em python __else__ junto com o comando __if__.

```bash
>>> produto = 33.00
>>> produto
33.0
>>> pago = 33.00
>>> pago
33.0
>>> pago - produto
0.0
>>> if( produto < pago ):
...     print('precisa de troco!')
... else:
...     print('não precisa de troco!')
...
não precisa de troco!
>>>

```

No bloco acima o comando __ELSE__ (i.e., SE NÃO) ele representa a contradição de algo acontecer ou que a expressão validada no comando __IF__ seja __FALSA__. No exemplo acima nos alteramos o valor de pago para a mesma quantia do valor do produto comprado por um cliente. No exemplo estudado, o que fizemos foi avaliar se o cliente iria precisar de troco e no exemplo acima ele não precisaria devido ao valor pago ser extamente igual ao do produto. No comando "if" a expressão gera um resultado FALSO logo, o comando "else" é acionado pois é a única coisa que pode acontecer na sequência. Muito simples não é mesmo?

Agora, vamos deixar as coisas mais quentes e aumentar a complexidade das condições mas, ainda sim tentar ver como isso ainda continua simples. Vamos imaginar uma brincadeira onde nos vamos guardar um número de 0 a 10 em uma variável e utilizando expressões if e else descobrir qual é esse número.

```bash
>>> numero = 7
>>> if(numero == 0):
...     print("o número informado foi o zero")
... elif (numero == 1):
...     print("o número informado foi o um")
... elif (numero == 2):
...     print("o número informado foi o dois")
... elif (numero == 3):
...     print("o número informado foi o três")
... elif (numero == 4):
...     print("o número informado foi o quatro")
... elif (numero == 5):
...     print("o número informado foi o cinco")
... elif (numero == 6):
...     print("o número informado foi o seis")
... elif (numero == 7):
...     print("o número informado foi o sete")
... elif (numero == 8):
...     print("o número informado foi o oito")
... elif (numero == 9):
...     print("o número informado foi o nove")
... else:
...     print("o número informado foi o dez")
...
o número informado foi o sete

```

No exemplo acima estamos usando um novo comando o elif. Esse comando ele serve para realizar a condição de __SE NÃO, SE__ de forma que sempre que não não aconteceu, o seguinte pode acontecer. Viu como foi fácil e simples entender estruturas condicionais.

Exercícios para praticar o que aprendeu:

1. Crie uma variável chamada __numero__ e informe um valor numérico para ela sendo que esse valor deve estar dentro do intervalo de 0 a 10. Verifique se o valor que você definiu é menor ou maior que 5.

2. Crie uma lista de nomes que contenha estes 6 nomes: Rafael, Joelson, Matheus, Ligia, Glenda e Mauricio. Verifique se os seguintes nomes Gabriel, Lucas, Matheus, Rafael, Glenda e Maria estão na lista criada. Se o nome existir na lista, utilizando o comando print imprimir na tela a seguinte frase "Nome esta na lista".

3. Crie duas variaveis que contenham dois números e imprima o maior deles.

4. Crie uma variável que contenha um valor (positivo ou negativo) e imprima na tela se o valor é positivo ou negativo.

5. Crie uma variável que contenha o caracter "F" ou "M". Conforme a letra informada verifique se: "F" imprima Feminino, "M" imprima Masculino e se algum outro caractere for informado imprima "Sexo Inválido".

6. Crie três variáveis: peso, altura e imc. você deve preencher a variável peso com o seu peso atual e a altura com a sua altura atual. A váriavel imc vai receber a seguinte expressão matemática:
```bash
>>> imc = peso / (altura ** 2)
```
Com o imc em mãos você vai construir condições para saber em que estado você se encontra atualmente. Para criar as condições você irá se basear com base na Tabela a seguir:

IMC |	Classificação
:------:|:------:
abaixo de 18,5 | abaixo do peso
entre 18,6 e 24.9 | peso ideal (parabéns)
entre 25,0 e 29.9 | levemente acima do peso
entre 30,0 e 34.9 | obesidade grau I
entre 35,0 e 39.9 | obesidade grau II (severa)
acima de 40 | obesidade III (mórbida)
