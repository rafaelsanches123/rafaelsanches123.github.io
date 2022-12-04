---
layout: post
title:  "Modelagem de Dados com Apache Cassandra"
date:   2022-12-03 13:27:01 -0300
categories: modelagem dados apache cassandra big-data nosql
---

![apache cassandra]({{ site.url }}/assets/apache-cassandra.png){:style="width: 100%" }

Fala pessoal blz? No post de hoje vamos trocar uma ideia sobre __Apache Cassandra__ e como modelar dados nesse banco de dados NOSQL que vem sendo bastante usada no universo do Big Data. E aí, bora aprender algo novo?

## O que é Apache Cassandra?

Segundo o site oficial do Cassandra, ele é um banco de dados distribuído NoSQL de código aberto, confiável que garante escalabilidade e alta disponibilidade sem comprometer o desempenho. Escalabilidade linear e tolerância a falhas comprovada em hardware de commodity (computadores de baixo custo) ou infraestrutura de nuvem o tornam a plataforma perfeita para dados de missão crítica.

Ainda segundo o site oficial do Apache Cassandra por design, os bancos de dados NoSQL são leves, de código aberto, não relacionais e amplamente distribuídos. Entre seus pontos fortes estão a escalabilidade horizontal, arquiteturas distribuídas e uma abordagem flexível para definição de esquema.

Os bancos de dados NoSQL permitem organização e análise rápidas e de tipos de dados diferentes e de volume extremamente alto. Isso se tornou mais importante nos últimos anos, com a chegada do Big Data e a necessidade de dimensionar rapidamente os bancos de dados na nuvem. O Apache Cassandra está entre os bancos de dados NoSQL que abordaram as restrições de tecnologias de gerenciamento de dados anteriores, como bancos de dados SQL.

Uma das vantagens do Apache Cassandra é sua capacidade de resiliencia, se você tiver um ponto de falha em algum nó do seu cluster os seus dados estaram replicados em outros nós garantindo um ambiente resiliente e de alta disponibilidade fornecendo a você mais segurança contra perda de dados.

Outra caracteristica super bacana do Apache Cassandra é a escalabilidade horizontal que é semelhante a do Apache Hadoop. Imagine que se você precisar de mais espaço e mais poder de processamento você pode incluir mais máquinas no seu cluster de acordo com a necessidade da sua aplicação/software.

## Como instalar/testar o Apache Cassandra

Se você quiser instalar o Apache Cassandra para testar na sua máquina use uma das opções a seguir:
* opção 1: [Site oficial](https://cassandra.apache.org/_/download.html);
* opção 2: [Usando docker](https://hub.docker.com/_/cassandra);
* opção 3: Usando docker-compose ->

```yaml
# docker-compose.yml
version: '2'

services:
  cassandra:
    image: cassandra:4.0
    ports:
      - 9042:9042
    volumes:
      - ./apps/cassandra:/var/lib/cassandra
    environment:
      - CASSANDRA_CLUSTER_NAME=cluster_rafael

```

Para qualquer dúvida sobre as opções usando docker recomendo que estude sobre o assunto caso não tenha nenhum conhecimento.



## Em construção... ##