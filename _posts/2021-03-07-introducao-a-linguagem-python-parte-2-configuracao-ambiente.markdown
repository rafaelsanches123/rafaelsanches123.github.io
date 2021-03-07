---
layout: post
title:  "Introdução a linguagem python parte 2 - Instalação e Configuração"
date:   2021-03-03 20:25:03 -0300
categories: python
---

![linguagem-python]({{ site.url }}/assets/linguagem-python.png){:style="width: 100%" }

## Instalando e configurando o python no seu computador

### Sistemas Operacionais Windows

Uma das formas mais simples de instalar o python, pode ser utilizando o ananconda que é um gerenciador de pacotes que já vem preparado com algumas bibliotecas do python ou somente o python de forma mais crú direto do site do python. Para usar o anaconda, basta acessar o site do [Anaconda](https://docs.anaconda.com/anaconda/install/windows/), baixar o arquivo executável de instalação referente ao seu sistema operacional windows (64bit ou 32bit) e clicar 2x no arquivo executável e ir clicando em próximo até finalizar o processo de instalação. Antes de finalizar o processo de instalação, se aparecer uma opção com checkbox para assinalar e conter a informação se você deseja vincular a sua instalação python a variavel __PATH__ de ambiente do windows pode marcar essa opção pois, isso te permitirá utilizar o python dentro do CMD do windows.

Se tiver alguma dúvida, apenas vá clicando em próximo sem se preocupar e sem medo de algo dar errado.

O processo acima também é válido para instalação somente do python sem bibliotecas adicionais. Para isso basta acessar o site do [Python](https://www.python.org/downloads/windows/) e fazer o mesmo processo supracitado.

### Sistemas Operacionais Linux

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

### Sistemas Operacionais MacOS

No MacOs a primeira coisa a se fazer é instalar o gerenciador de pacotes do MacOs o __HomeBrew__. Para isso acesse o site com todos os passos para necessários [HomeBrew](https://brew.sh/). Depois de instalar o HomeBrew, basta abrir um terminal e digitar o comando a seguir:
```
brew install python3
```

### Python pelo navegador do seu computador, tablet ou smartphone

Se você não quiser instalar o python na sua máquina por meio dos métodos acima por ter algum medo, você poder usar alguns dos sites a seguir para rodar o python no seu navegador e poder fazer esse curso introdutório:

* [Repl.it](https://repl.it/languages/python3)
* [IDEONE](https://ideone.com/)

Se você conhece mais algum outro site que não listei acima, menciona ele nos comentários que eu adiciono ele na lista acima.

Bora lá então se você for utilizar algum dos listados acima para fazer esse curso, eu recomendaria o [Repl.it](https://repl.it/languages/python3) eu acho ele melhor e mais fácil de utilizar.

A seguir, temos uma imagem do [Repl.it](https://repl.it/languages/python3) e alguns apontamentos de como utilizar ele para esse curso:

![python-web-repl.it]({{ site.url }}/assets/repl-it-languages-python3.png){:style="width: 100%" }
***Figura 1***: *Exemplo de ambiente web alternativo para programar em python*

A própria imagem acima fala por si só não é mesmo? Na parte esquerda do site, você cria os seus scripts com a extensão __.py__. No meio do site, fica a região na qual representa um editor de textos para python e ele vai colorir seus códigos e ajudar você a visualizar melhor seus comandos python. Na parte a direita do site, fica o __terminal__ e é nele que vai aparecer o resultado do que codificarmos. Você pode escrever seus códigos no editor no bloco central do site e depois que escrever seu código você deve executar ele e para isso você dever clicar no botão __Run__ que fica logo acima do nosso editor. Após clicar nele seu código será interpretado e o resultado irá aparecer no seu terminal.

Outra alternativa também é escrever seus códigos diretamente do terminal. Mas ai fica a seu critério essa escolha.
