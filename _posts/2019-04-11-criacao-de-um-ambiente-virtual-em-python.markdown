---
layout: post
title:  "O que é um ambiente virtual em python? Para que isso serve?"
date:   2019-04-11 05:10:03 -0300
categories: python
---

![ambiente virtual]({{ site.url }}/assets/ambiente-virtual.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou mostrar para vocês o funcionamento do incrível __virtualenv__, uma ferramenta simples e poderosa que permite criar ambientes isolados de desenvolvimento na linguagem python, ou seja, torna possível a utilização de diversas bibliotecas em um mesmo ambiente sem que haja conflitos entre elas e também o mesmo ambiente pode ser reutilizado por outras pessoas permitindo que elas usem as mesmas configurações.

## Como esse __virtualenv__ funciona?

O funcionamento do virtualenv é algo bastante simples. Ele basicamente constrói uma cópia de todos os diretórios necessários para que um programa python seja executado, isto inclui:
* As bibliotecas comuns do python (*standard library*);
* O gerenciador de pacotes pip;
* O próprio binário do python seja ele da versão 2.x ou 3.x;
* Dependências que estiverem no diretório do __pacote desejado__ instalado (e.g., __numpy__ ou qualquer outra);
* Seu código fonte descrevendo sua aplicação.

Desse modo ao instalar uma nova dependência (i.e., biblioteca) dentro do ambiente criado pelo __virtualenv__, essa dependência será colocada no diretório de __pacotes local__ relativo à esse ambiente, e não mais globalmente.

Assim, só esse ambiente visualiza essa dependência!

### Passo a passo para utilização de um ambiente virtual em python

Para instalar o __virtualenv__ você precisa ter o __pip__ instalado na sua máquina. O __pip__ nada mais é do que o __gerenciador de pacotes__ do __python__ assim como no __java__ tem o __maven__, no __nodejs__ tem o __npm__ e __yarn__ e no __php__ tem o __composer__.

Para instalar o pip para o python 2 no sistema linux distro ubuntu digite no terminal:
```
sudo apt install python-pip
```

Para instalar o pip para o python 3 no sistema linux distro ubuntu digite no terminal:
```
sudo apt install python3-pip
```

Agora com o pip instalado, precisamos executar apenas um comando para instalar o __virtualenv__:

```
Para o python 2:
sudo pip install virtualenv

Para o python 3:
sudo pip3 install virtualenv
```

Agora você já pode começar a criar seus ambientes virtuais em python!

#### __Inicializando um ambiente virtual__

No terminal acesse um diretório no qual você deseja criar seu ambiente e então digite o seguinte comando:
```
Desse modo se você não especificar o python ele irá criará um ambiente virtual para o python 2:
virtualenv nome_do_seu_ambiente_virtual

Por exemplo:
virtualenv ambiente_virtual

Outra alternativa para especificar a versão do python caso a anterior não seja do seu agrado:
virtualenv --python=/usr/bin/python3 nome_do_seu_ambiente_virtual
```

Esse comando cria um novo ambiente de desenvolvimento totalmente isolado e nesse caso, vamos chamar nossa pasta de __ambiente_virtual__.

Nesse ambiente/pasta são criados alguns diretórios importantes como:

* __ambiente_virtual__/lib e __ambiente_virtual__/include: contêm as bibliotecas de suporte ao ambiente virtual. Os pacotes baixados via pip por exemplo serão instalados em __ambiente_virtual__/lib/pythonX.X/pacotes-locais/ (não mais globalmente).

* __ambiente_virtual__/bin: residem os binários necessários para executar o próprio __python__, entre outros executáveis (e.g., como o pip ou setuptools). Dessa forma, os comandos python script.py e __ambiente_virtual__/bin/python script.py produzem exatamente o mesmo resultado.

#### __Ativando um ambiente virtual__
__Toda vez__ que você __desejar acessar o ambiente virtual criado__ é necessário que você o __ative__. Para isso basta digitar o seguinte comando:
```
Linux/MacOs:
source ambiente_virtual/bin/activate

Windows:
ambiente_virtual\Scripts\activate
```

Com seu ambiente virtual ativado você pode instalar as bibliotecas necessárias para o funcionamento do seu projeto.

Se você deseja instalar uma biblioteca que precisa utilizar em seu projeto faça da seguinte maneira:
```
pip install nome_do_pacote
```
Portanto, o nome do pacote deve ser exatamente como ele se encontra no site do __pip__. Ele baixará todos os arquivos necessários e instalará esse pacote.

Então, se você quiser remover um pacote do python instalado via pip, você pode usar a opção que remove bibliotecas em pip.
```
pip uninstall nome_do_pacote
```

Viu como é simples!

#### __Desativando um ambiente virtual__
Para desativar um ambiente virtual digite no terminal onde o ambiente virtual está ativado/aberto:
```
deactivate
```

#### __Gerar arquivo com as bibliotecas utilizadas no projeto com suas respectivas versões__
Com o ambiente virtual ativado e na raiz do projeto digite no terminal o comando:
```
pip freeze > requirements.txt
```
requirements.txt é o nome do seu arquivo.txt que contêm as dependências do seu projeto python.

#### __A partir de um arquivo como o especificado no tópico acima instalar todas dependências de um projeto python a partir de um arquivo com a extensão .txt__
Para instalar todas as dependências, esteja com o seu ambiente virtual ativado e no terminal digite o comando:
```
pip install -r /caminho-do-arquivo/requirements.txt
```
