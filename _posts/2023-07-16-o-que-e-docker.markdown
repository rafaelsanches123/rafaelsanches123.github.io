---
layout: post
title:  "O que é o docker?"
date:   2023-07-16 10:00:00 -0300
categories: docker
---

![docker]({{ site.url }}/assets/docker.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre uma ferramenta que chegou para ajudar muitos desenvolvedores com aquele famoso problema "Na minha máquina funciona". Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

## Docker

O __Docker__ é uma __plataforma de código aberto__ que permite a criação, distribuição e execução de aplicativos em __contêineres__. Contêineres são unidades de software leves e portáteis que contêm tudo o que é necessário para executar um aplicativo, incluindo o código, as dependências, as bibliotecas e as configurações do sistema.

O __Docker__ foi projetado para tornar o __desenvolvimento__, __implantação__ e __escalonamento__ de aplicativos mais __rápidos__ e __eficientes__, oferecendo uma abordagem __consistente__ e __confiável__ para empacotar e executar aplicativos em __diferentes ambientes__.

Principais __conceitos__ do Docker:

1.  __Imagens Docker__: Uma imagem Docker é um pacote autossuficiente que contém o código do aplicativo, suas dependências e outras configurações necessárias para executar o aplicativo. As imagens são criadas a partir de um arquivo chamado Dockerfile, que descreve os passos para construir a imagem.

2.  __Contêineres Docker__: Um contêiner é uma instância em execução de uma imagem Docker. Os contêineres são isolados uns dos outros e do sistema hospedeiro, o que garante a portabilidade e a independência das aplicações. Cada contêiner tem seu próprio ambiente de execução, mas compartilha o mesmo kernel do sistema operacional do host.

3.  __Docker Hub__: É um registro público de imagens Docker, onde você pode encontrar imagens prontas para uso e compartilhar suas próprias imagens com a comunidade. O [Docker Hub](https://hub.docker.com/) é uma fonte valiosa de imagens para acelerar o processo de desenvolvimento e implantação.

## Vantagens do Docker:

1.  __Portabilidade__: Os contêineres são portáteis e podem ser executados em qualquer ambiente que tenha o Docker instalado, garantindo que os aplicativos se comportem de forma consistente em diferentes plataformas.

2.  __Isolamento__: Os contêineres são isolados uns dos outros e do sistema hospedeiro, o que evita conflitos de dependências e garante que as aplicações não interfiram entre si.

3.  __Eficiência__: O Docker usa recursos do sistema de forma mais eficiente, pois os contêineres compartilham o mesmo kernel do sistema operacional, evitando a sobrecarga de máquinas virtuais tradicionais.

4.  __Escalabilidade__: Os contêineres podem ser dimensionados rapidamente, facilitando o escalonamento horizontal de aplicativos com base na demanda.

O __Docker__ tornou-se uma ferramenta essencial para muitos desenvolvedores e equipes de DevOps, facilitando o processo de empacotamento, distribuição e implantação de aplicativos, além de proporcionar um ambiente consistente para o desenvolvimento e teste.