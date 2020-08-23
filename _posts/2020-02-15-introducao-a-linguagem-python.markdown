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

2. Criar uma variável chamada idade e atribuir a sua idade a ela.

3. Criar uma variável chamada camiseta e atribuir um valor flutuante (i.e., valor quebrado) a ela.

4. Criar uma variável chamada felicidade e atribuir um valor booleano a ela.

5. Criar uma variável chamada amigos e atribuir cinco nomes de amigos utilizando listas a ela.

6. Criar uma variável chamada funcionário e atribuir um dicionário a ela com suas informações tais como: nome, idade, email e telefone.

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

## Operadores Lógicos, Aritméticos e Relacionais

__Operadores Lógicos__:
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
Outros dois operadores lógicos ainda não mencionados mas, muito utilizados no python são: __not__ e o __in__. O operador not é geralmente utilizado para negar uma expressão booleana por exemplo:

```bash
>>> A = True
>>> not A
False
>>> A
True
>>> B = False
>>> B
False
>>> not B
True
>>>

```

Muito simples não é mesmo?

O operador in ele é uma ferramenta muito interessante quando temos que verificar se algo existe ou não dentro de alguma variável de tipo heterogênea como strings, listas, etc...

Vamos ver ele na prática como funciona e ver como ele é simples:

```bash
>>> lista_frutas = ['uva','maçã','limão','jaca']
>>> 'uva' in lista_frutas
True
>>> 'laranja' in lista_frutas
False
>>> frase = "eu trabalho na empresa serasa e gosto de computadores"
>>> 'empresa' in frase
True
>>> 'valor' in frase
False
>>> 'Rafael' in frase
False
>>> 'computador' in frase
True
>>> 'computaçao' in frase
False
>>>

```

__Operadores Aritméticos__:
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

__Operador Relacionais__:
É todo operador que obtém a relação do membro a esquerda com o membro a sua direita. Na tabela abaixo, temos os operadores relacionais disponibilizados pelo python.

Descrição |	Operador
:------:|:------:
Maior que |	>
Menor que |	<
Igual a | ==
Diferente a | !=
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

>>> 10 != 2
True

>>> 10 >= 2
True

>>> 10 <= 2
False

```

Exercícios para praticar o que aprendeu:

1. Criar uma variável e chamada de __maior_valor__ e atribuir a ela o valor 10. Criar uma variável e chamada de __menor_valor__ e atribuir a ela o valor 3.

2. Usando o operador de __igual a__ verificar se o valor de __maior_valor__ é igual ao conteúdo da variável __menor_valor__.

3. Usando o operador de __diferente a__ verificar se o valor de __maior_valor__ é igual ao conteúdo da variável __menor_valor__ ou se os valores são diferentes.

4. Usando o operador __maior que__ verificar se o valor de __maior_valor__ é maior que o conteúdo da variável __menor_valor__.

5. Usando o operador __menor que__ verificar se o valor de __maior_valor__ é menor que o conteúdo da variável __menor_valor__.

6. Usando o operador __subtração__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

7. Usando o operador __multiplicação__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

8. Usando o operador __divisão__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

9. Usando o operador __parte inteira__ calcular o resultado entre  __maior_valor__ e __menor_valor__.

10. Usando o operador __módulo__ calcular o resultado entre  __maior_valor__ e o número 2 e verificar se o resultado gerado é diferente de zero. (Se o resultado gerado for zero significado que __maior_valor__ é par).

11. Usando o operador __módulo__ calcular o resultado entre  __menor_valor__ e o número 2 e verificar se o resultado gerado é diferente de zero. (Se o resultado gerado for zero significado que __menor_valor__ é par).

12. Crie um lista de comprar e nela adicione 5 produtos que você costuma comprar no mercado. Usando o operador __in__ use 3 produtos que você não adicionou na sua lista e depois faça a mesma coisa para 2 produtos que você colocou na sua lista.

13. Utilizando o operador __not__ aplique ele para o valor 1 e depois para o valor zero e veja o que ele retorna para cada um desses valores.


## Estruturas condicionais

Durante o fluxo de algum raciocínio humano ocorre-se a necessidade de tomar uma decisão se, certa condição ocorrer e de tomar outra decisão se alguma outra coisa ocorrer. Na linguagem python quando você tem essas mesmas necessidades costuma-se utilizar a palavra __if__ e __else__ dependendo do que se deseja alcançar e também a casos em que você queira ter mais de uma condição seguida dependendo que deseja analisar.



Para deixar isso mais claro vamos ver como isso ocorre na pratica:

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

Acima podemos ver 2 comandos novos a estrutura de condição simples __if__ que nos ajuda a analisar uma expressão e se essa expressão resulta em verdade ela será realizada se não, não acontecerá nada no caso acima é claro. Ainda no exemplo acima foi possível observar o comando __print__. O comando print ele tem a função de imprimir o algo na tela do seu computador seja um texto simples, composto ou mesmo o conteúdo de alguma variável. Não se preocupe pois, vamos utilizar ele bastante no decorrer desse post para visualizar nossas ações ou apresentar respostas na tela do computador.

Existem certas ocasiões que se algo não acontecer outra decisão precisa ser tomada. Seguindo ainda o mesmo exemplo do troco imagine que agora o cliente pagou o valor exato do produto no caixa e ele não vai precisar receber troco nesse caso podemos expressar isso utilizando estruturas condicionais utilizando o termo __else__ junto com o comando __if__.

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

## Laços de repetição

Os lações de repetição são utilizados na maioria das vezes para realizar repetições que podem ser previamente conhecidas ou não dependendo que você deseja realizar. Uma aplicação bastante realizada por meio de repetições por exemplo ocorre quando eu tenho uma lista de itens e eu desejo saber todos esse itens. Ou enquanto algo não ocorrer eu continuo repetindo algum bloco de comando até que tal condição seja satisfeita.

No python nos temos os seguintes comandos de laço de repetição sendo eles o: __for__ e o __while__.

o laço de repetição __for__: ele é geralmente utilizado quando eu sei a quantidade de repetições a serem realizadas.

o laço de repetição __while__: ele é geralmente utilizado quando eu não sei o número de repetições a serem realizadas.

Vamos entender isso um pouco mais. Vamos imaginar que o professor Rafael te passou uma lição para casa e você não a fez. Como castigo o professor Rafael lhe pediu para que escrever na losa o seu nome dele 10 vezes para que você não esqueça mais de fazer a lição de casa. Poxa vida mas que coisa chata, é verdade eu também pensei o mesmo.

No mundo digital isso não precisa ser chato basta, utilizar o laço __for__ para nos ajudar nessa tarefa. Ok mas o que eu faço? vamos lá:

```bash
>>> for i in range(0,10):
...     print("Rafael")
...
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
Rafael
>>>
```
Vamos entender o código acima e também o que o comando novo que surgiu faz. A estrutura do comando for é bastante simples de forma falada o que ele faz é: "Para" cada valor "i" iniciando a partir de "0" até "10" faça. De forma bastante sucinta é exatamente isso que ele faz. O comando __range__ nada mais é do que uma __função__ algo que será visto mais a frente que cria para você uma lista de números que vai de 0 até 9 exatamente. A variável i após o comando for para cada iteração ela recebe o conteudo gerado pela função range.

Agora, vamos replicar a mesma ideia acima só que uma pitada a mais de conhecimento utilizando o comando __enumerate__ e pega uma lista ou outro tipo de coleção de dados e lhe retorna o indice e o valor referente aquele indice. Vamos por a mão na massa para entender isso melhor:

```bash
>>> numeros = range(0,10)
>>> numeros
range(0, 10)
>>> for indice, valor in enumerate(numeros):
...     print("indice:",indice,"valor:",valor)
...
indice: 0 valor: 0
indice: 1 valor: 1
indice: 2 valor: 2
indice: 3 valor: 3
indice: 4 valor: 4
indice: 5 valor: 5
indice: 6 valor: 6
indice: 7 valor: 7
indice: 8 valor: 8
indice: 9 valor: 9

>>> for indice, valor in enumerate(numeros):
...     print("indice:",indice,"valor:",valor,"Rafael")
...
indice: 0 valor: 0 Rafael
indice: 1 valor: 1 Rafael
indice: 2 valor: 2 Rafael
indice: 3 valor: 3 Rafael
indice: 4 valor: 4 Rafael
indice: 5 valor: 5 Rafael
indice: 6 valor: 6 Rafael
indice: 7 valor: 7 Rafael
indice: 8 valor: 8 Rafael
indice: 9 valor: 9 Rafael
>>>

```

No exemplo acima como ainda estamos utilizando sequência numérica o indice tem o mesmo valor que o seu conteudo. Para deixar isso mais claro vamos ver um exemplo com uma lista de frutas e exibir cada fruta e seus respectivo indice referente a sua posição na lista.

```bash
>>> lista_frutas = ['maça','pera','morango','limão','banana','uva']
>>> for fruta in lista_frutas:
...     print("Nome fruta:", fruta)
...
Nome fruta: maça
Nome fruta: pera
Nome fruta: morango
Nome fruta: limão
Nome fruta: banana
Nome fruta: uva
>>>
```

```bash
>>> for indice,valor in enumerate(lista_frutas):
...     print("posicao da fruta na lista:", indice, "Nomde da fruta:", valor)
...
posicao da fruta na lista: 0 Nomde da fruta: maça
posicao da fruta na lista: 1 Nomde da fruta: pera
posicao da fruta na lista: 2 Nomde da fruta: morango
posicao da fruta na lista: 3 Nomde da fruta: limão
posicao da fruta na lista: 4 Nomde da fruta: banana
posicao da fruta na lista: 5 Nomde da fruta: uva
>>>

```

Simples não é mesmo?

Agora vamos entender melhor o laço de repetição __while__. O comando __while__ faz com que um conjunto de instruções seja executado enquanto uma condição é atendida. Quando o resultado dessa condição passa a ser falso, a execução do loop é interrompida, como mostra o exemplo a seguir.

```bash
>>> contador = 0
>>> while (contador < 10):
...        print(contador)
...        contador   = contador + 1
...
0
1
2
3
4
5
6
7
8
9
```
No código acima eu inicializei uma variável chamanda de contador com o valor zero e na linha seguinte eu uso o comando while seguido de uma expressão booleana que enquanto ela continuar sendo verdadeira o laço de repetição irá continuar acontecendo. No caso do exemplo acima a condição diz que __ENQUANTO__ o conteúdo da variável contador for menor que dez o laço de repetição deve ser executado.
Nesse exemplo a cada execução é apresentado ao usuário o valor corrente da variável contador naquele momento e na sequência ele tem seu valor alterado para que em determinado momento o laço seja interrompido e por consequência finalizado. Se por algum acaso a sua condição sempre gerar resultado verdadeiro você irá cair no que chamamos de loop infinito ou laço de repetição sem fim. Evite que isso aconteça, pois leva ao congelamento e finalização da aplicação/programa de computador.

A seguir veja um exemplo utilizando entrada de dados.

```bash
>>> numero = int(input("Informe um número entre 1 a 10\n"))
Informe um número entre 1 a 10
2
>>> while(numero > 0 and numero <=10):
...     print("Você informou o número: {}".format(numero))
...     numero = int(input("Informe um número entre 1 a 10\n"))
...
Você informou o número: 2
Informe um número entre 1 a 10
2
Você informou o número: 2
Informe um número entre 1 a 10
5
Você informou o número: 5
Informe um número entre 1 a 10
0

```
Veja que interessante o código acima. Nele é solicitado um número ao usuário e enquanto esse número informado pelo usuário for maior que zero e menor ou igual a dez o computador irá ficar solicitando ao usuário um número desde que ele atenda a condição do laço while.

```bash
>>> numero = int(input("Informe um número entre 1 a 10\n"))
Informe um número entre 1 a 10
1
>>> print(numero)
1
>>> while(numero > 0 and numero <=10):
...     print("Você informou o número: {}".format(numero))
...     numero = int(input("Informe um número entre 1 a 10\n"))
... else:
...     print("Você informou o número: {} e ele está fora da condição estabelecida".format(numero))
...
Você informou o número: 1
Informe um número entre 1 a 10
5
Você informou o número: 5
Informe um número entre 1 a 10
6
Você informou o número: 6
Informe um número entre 1 a 10
4
Você informou o número: 4
Informe um número entre 1 a 10
11
Você informou o número: 11 e ele está fora da condição estabelecida

```

O código acima é exatamente igual ao anterior mas com o diferencial do comando __else__ eu particularmente nunca utilizei ele com laço de repetição while mas, se em algum momento você precisar fica ai mais uma forma de utilizar ele no seu dia a dia se for da sua vontade e necessidade.

Exercícios para praticar o que aprendeu:

1. Com a ajuda de uma laço de repetição, solicite ao usuário um número inteiro e a cada iteração desse laço. O número de repetições deve ser 10. A cada iteração imprimir na tela a sequência do laço e o número que o usuário informou naquela iteração.

2. Faça um programa similar ao programa do exercício 1 acima. Nesse novo programa, ao final da execução desse laço de repetição você precisa imprimir na tela do usuário qual foi o menor número informado durante a execução do laço de repetição.

3. Faça um programa similar ao programa do exercício 2 acima. Nesse novo programa, ao final da execução desse laço de repetição você precisa imprimir na tela do usuário qual foi o maior número informado durante a execução do laço de repetição.

4. Solicite ao usuário dois números inteiros e imprimir na tela do usuário os números entre os dois números solicitados. Ex: n1=2 e n2=5 caso você use esses dois número o deverá aparecer na tela do usuário a seguinte sequência: 2, 3, 4, 5.

5. Faça um programa similar ao programa do exercício 4 acima. Nesse novo programa, você deve imprimir no final da sequência solicitada ao usuário o somatório dessa sequência.

6. Com a ajuda de um laço de repetição realize 20 repetições e imprima na tela do usuário somente as posições impares.

7. Com a ajuda de um laço de repetição realize 30 repetições e imprima na tela do usuário somente as posições pares.

8. Com a ajuda de um laço de repetição, fique solicitando um valor inteiro ao usuário a cada iteração do laço. O laço de repetição nesse exercício só deve terminar quando o usuário informar um valor inteiro negativo.

9. Desenvolva um programa gerador de tabuada, capaz de gerar a tabuada de qualquer número inteiro entre 1 a 10. O usuário deve informar de qual numero ele deseja ver a tabuada. A saída deve ser conforme o exemplo abaixo:
Tabuada de 5:
5 X 1 = 5
5 X 2 = 10
...
5 X 10 = 50

10. O desafio mais dificil desse estágio: __Fibonacci__ é uma sequência de números, que aparece em certos mistérios da natureza e da vida, onde a sequência inicia com 0 e 1, e os números seguintes serão a soma dos dois números anteriores.

Por exemplo: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55…

Faça um programa capaz de gerar a série de Fibonacci até o n−ésimo termo ou seja, solicite um número inteiro ao usuário e dado esse número gerar a série de Fibonacci até essa posição da sequência. Por exemplo, se o usuário solicitar a 7ª você deve gerar a sequência 0, 1, 1, 2, 3, 5, 8 na tela do usuário.

## Strings

Em construção...

## Estruturas de dados

Em construção...

## Funções

Em construção...

## Módulos

Em construção...
