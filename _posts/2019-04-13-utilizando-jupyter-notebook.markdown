---
layout: post
title:  "Utilizando jupyter notebook com python"
date:   2019-04-13 07:00:00 -0300
categories: python
---

![jupyter notebook]({{ site.url }}/assets/jupyter.svg){:style="width: 100%;max-height: 400px" }

## Jupyter notebook

Fala pessoal blz? Nesse post, vou mostrar para vocês o funcionamento do incrível __jupyter notebook__, uma ferramenta simples e muito poderosa que permite você aprender a programar nas linguagens Python, Ruby, R, C++ e Julia, ou seja, torna possível a codificação e visualização do que foi programado por meio de um browser (i.e., navegador).

O [link oficial](https://jupyter.org/) do jupyter notebook para quem quiser dar uma olhada. O jupyter notebook tem sido muito utilizado no ensino da programação. O professor/instrutor pode montar sua aula diretamente no notebook criado pelo jupyter e nele colocar textos usando a linguagem de marcação de texto markdown de modo muito simples e rápido. Se você não desejar instalar essa ferramenta localmente na sua máquina, você pode utilizar ela na sua versão web diretamente pelo seu browser acessando o link [try jupyter](https://jupyter.org/try) e clicando sobre a linguagem que desejar utilizar.

O jupyter notebook tem sido bastante utilizado com a linguagem python por cientistas de dados. Isso facilita a geração de relatórios e agiliza o processo de apresentar/atualizar resultados em tempo real dependendo do que sua aplicação faça. 

A seguir, vou apresentar como configurar e utilizar essa ferramenta com a linguagem python para que você caro leitor, possa começar a se divertir e aprender uma nova linguagem de programação.


## Configurando o jupyter notebook para utilizar a linguagem python

Se você quiser utilizar um ambiente fechado para testar o jupyter recomendo que veja o artigo [link para o artigo]({% post_url 2019-04-11-criacao-de-um-ambiente-virtual-em-python %}) para ver como utilizar um ambiente virtual fechado em projetos python. Se não, pode continuar a leitura.

Se você usa o Python 3 (que é o recomendado atualmente pelo próprio site do jupyter):

Abra o terminal e digite:
```
python3 -m pip install --upgrade pip
python3 -m pip install jupyter
```

ou

Se você usa o  Python 2:

Abra o terminal e digite:
```
python -m pip install --upgrade pip
python -m pip install jupyter
```

Se tudo ocorreu bem, basta abrir o terminal e digitar:
```
jupyter notebook
```

Simples não é mesmo? Depois que o jupyter abrir em seu browser basta criar um notebook dar um nome a ele e começar a programar!