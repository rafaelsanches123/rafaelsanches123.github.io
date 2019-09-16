---
layout: post
title:  "Extraindo texto de imagens com python"
date:   2019-09-14 10:10:03 -0300
categories: python
---

![python-ocr-pytesseract]({{ site.url }}/assets/tesseract-ocr-e-python.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre uma tecnologia poderosíssima que podemos utilizar com __python__ para extrair textos de dentro de imagens. Essa tecnologia é geralmente conhecida como __OCR__! Mas o que seria um OCR?

Optical Character Recognition (__OCR__) é uma tecnologia para reconhecer caracteres a partir de um arquivo de imagem. Então, por meio do OCR é possível obter um arquivo de texto editável por um computador.

Para conseguirmos realizar essa proeza, vamos precisar então de ter em nossa máquina uma ferramenta de OCR e nesse caso, a escolhida para ser utilizada nesse post será o Tesseract.

O Tesseract foi originalmente desenvolvido na __Hewlett-Packard__ (HP) Laboratories Bristol e na HP Co, Greeley Colorado, entre os anos de 1985 à 1994. Em 1996 foi portado para Windows e em 2005 o Tesseract foi liberado a comunidade pela HP e desde 2006 é então desenvolvido pela gigante __Google__. Se a curiosidade bater, de uma olhada em seu repositório no [github](https://github.com/tesseract-ocr/tesseract).

O Tesseract por natureza é uma aplicação de terminal e a sua API disponibilizada para desenvolvimento é a __libtesseract__ possui suporte apenas para as linguagens C/C++. Para conseguirmos utilizar essa ferramenta com python, nós utilizaremos uma biblioteca chamada __pytesseract__. Escolhida neste post por sua facilidade e alta abstração de funções disponibilizadas dentro do Tesseract.
Sua grande vantagem é que trabalha com argumentos do tipo __Python Image Library__ (PIL). O suporte ao PIL possibilita a compatibilidade a todos os formatos de imagem suportados como os formatos jpeg, png, gif, bmp, tiff entre outros. Além disso, ela aceita uma grande variedade de extensões nativamente não suportadas no tesseract que por natureza aceita somente os formatos tiff e bmp.

Nesse post vamos realizar todo processo utilizando o sistema operacional linux com a distro Ubuntu na versão 18.04 e python 3.

## Instalando tesseract no Ubuntu

Primeiro vamos começar pela instalação do __Tesseract OCR__. Abra o terminal e digite o seguinte comando:

```
sudo apt-get install tesseract-ocr tesseract-ocr-por
```

## Instalando as bibliotecas a serem utilizadas com o python

Antes de começar a instalar as bibliotecas, recomendo fortemente que leia o artigo sobre ambientes virtuais. Essa leitura é recomendada porque vai te ajudar bastante em questão de organização de projetos [link para o artigo]({% post_url 2019-04-11-criacao-de-um-ambiente-virtual-em-python %}). Obs: se você estiver seguindo esse post sem utilizar um ambiente virtual, será importante trocar os comandos __pip__ por __pip3__.

Instalação do __biblioteca Pillow__. Abra o terminal e digite o seguinte comando:

```
pip install pillow
```
Instalação do __biblioteca Pytesseract__. Abra o terminal e digite o seguinte comando:

```
pip install pytesseract
```

Agora, abra seu editor de código ou IDE favorito e crie o arquivo python-ocr.py e salve dentro de algum diretório. No mesmo diretório salve a imagem a seguir com o nome __teste-com-python-ocr__ e use extensão __jpg__.

![imagem-de-exemplo-para-teste]({{ site.url }}/assets/imagem-teste-com-ocr.jpg){:style="width: 100%" }

Agora, depois de ter baixado a imagem para o mesmo diretório do seu código python, precisamos codificar nosso exemplo. Abra o arquivo .py que você criou e digite:

{% highlight python linenos %}
# Importando o módulo Pillow (Manipulação de Imagens) para abrir a imagem no script
from PIL import Image
# Módulo para a utilização da tecnologia OCR
import pytesseract
# Extraindo o texto da imagem
print( pytesseract.image_to_string( Image.open('teste-com-python-ocr.jpg'), lang='por') )
{% endhighlight %}

Agora, abra seu terminal dentro do diretório onde se encontra seu código .py e a imagem que baixou e digite o seguinte comando:

```
Se estiver dentro do ambiente virtual use:
python python-ocr.py

Se ambiente virtual use:
python3 python-ocr.py
```

Resultado gerado:
```
1 PÁGINA

TRADUÇÃO

Português - Inglês
```

Simples não é mesmo? Vale ressaltar que nem sempre o texto resultante é 100% correto, a tecnologia OCR depende muito da qualidade da imagem e da quantidade de detalhes que a mesma possui. Para tentar corrigir esses possiveis problemas, existem algumas técnicas usadas para fazer melhorias na imagem diminuindo a chance de erros na hora da extração em um outro post tentarei falar mais sobre essas abordagens de correção.
