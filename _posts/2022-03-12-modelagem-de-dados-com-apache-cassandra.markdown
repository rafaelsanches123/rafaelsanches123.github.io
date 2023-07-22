---
layout: post
title:  "Modelagem de Dados com Apache Cassandra"
date:   2022-12-03 13:27:01 -0300
categories: modelagem dados apache cassandra big-data nosql
---

![apache cassandra]({{ site.url }}/assets/apache-cassandra.png){:style="width: 100%" }

Fala pessoal blz? No post de hoje vamos trocar uma ideia sobre __Apache Cassandra__ e como modelar dados nesse banco de dados NOSQL que vem sendo bastante usada no universo do Big Data. E aí, bora aprender algo novo?

## O que é Apache Cassandra?

O Apache Cassandra é um banco de dados distribuído de código aberto altamente escalável, projetado para lidar com grandes volumes de dados, fornecendo alta disponibilidade e desempenho. Ele foi desenvolvido pelo Facebook e posteriormente doado para a Apache Software Foundation, onde se tornou um projeto de código aberto.

Principais características do Apache Cassandra:

* __Distribuído e Descentralizado__: O Cassandra é projetado para ser executado em um cluster de vários nós, em vez de um único servidor centralizado. Cada nó é igualmente importante e responsável por parte dos dados, garantindo assim a descentralização e a escalabilidade horizontal.

* __Alta Disponibilidade__: O Cassandra garante alta disponibilidade de dados usando replicação. Cada partição de dados é replicada em vários nós, garantindo que os dados permaneçam acessíveis mesmo em caso de falha de um ou mais nós.

* __Modelo de Dados Denormalizado__: Ao contrário dos bancos de dados relacionais que adotam a normalização para evitar a redundância de dados, o Cassandra favorece um modelo de dados denormalizado. Isso permite que os dados sejam duplicados em várias tabelas para otimizar o acesso e o desempenho das consultas.

* __Estrutura de Coluna Ampla (Wide-Column Store)__: O Cassandra é uma implementação de banco de dados do tipo coluna ampla, o que significa que os dados são armazenados em colunas em vez de linhas. Isso permite consultas rápidas e eficientes, pois o Cassandra pode recuperar apenas as colunas necessárias em vez de ler linhas inteiras.

* __Consistência Ajustável__: O Cassandra oferece diferentes níveis de consistência para leituras e gravações. Você pode ajustar o nível de consistência com base nos requisitos de disponibilidade e desempenho do seu aplicativo.

* __Sem Ponto Único de Falha__: Como o Cassandra é projetado para ser distribuído, não há um único ponto de falha. Cada nó no cluster é capaz de atender às solicitações e garantir a integridade dos dados.

* __Suporte a Clusters Multirregionais__: O Cassandra suporta clusters multirregionais, permitindo que os dados sejam replicados em diferentes regiões geográficas para melhorar a disponibilidade e a latência em escala global.

Devido a essas características, o Apache Cassandra é amplamente utilizado em cenários onde a escalabilidade, a disponibilidade e o desempenho são fundamentais, como em aplicativos da web, Internet das Coisas (IoT), análise de big data e muito mais. Ele fornece uma solução poderosa para armazenamento e recuperação de dados em larga escala, onde a consistência e a tolerância a falhas são essenciais.



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


## Sobre a modelagem de dados

A modelagem de dados no Apache Cassandra é um processo fundamental para projetar o esquema de armazenamento de dados em um banco de dados distribuído. Diferentemente dos bancos de dados relacionais, o Cassandra utiliza uma abordagem baseada em colunas amplamente conhecida como "wide-column store". A modelagem de dados no Cassandra requer um entendimento claro do modelo de dados subjacente para garantir um desempenho eficiente e escalabilidade horizontal.

Aqui estão os principais conceitos e características da modelagem de dados no Apache Cassandra:

1.  Chaves primárias e particionamento:
* Cada tabela no Cassandra __possui uma chave primária__ que consiste em uma ou mais colunas. A chave primária é usada para determinar como os dados serão particionados e distribuídos em todo o cluster.
* A chave primária é composta por duas partes: __a partição__ e a __chave de cluster__. A partição é usada para distribuir os dados em nós diferentes, enquanto a chave de cluster é usada para determinar a ordem dos dados dentro de cada partição.

2.  Distribuição e replicação:
* O Cassandra é projetado para ser um __banco de dados distribuído__, onde os dados são divididos em partições e distribuídos em diferentes nós. Isso permite que o Cassandra seja __altamente escalável e resiliente__.
* O número de réplicas de cada partição pode ser configurado, o que garante a disponibilidade dos dados em caso de falhas de nós. O Cassandra usa o modelo "__peer-to-peer__", onde __todos os nós__ têm a __mesma importância e responsabilidade__.

3. Modelo de dados denormalizado:
* Ao contrário dos bancos de dados relacionais, onde a normalização é comum para evitar a redundância de dados, o Cassandra adota uma __abordagem denormalizada__. Os dados são armazenados de forma redundante para otimizar o acesso e o desempenho das consultas.
* É comum duplicar dados em várias tabelas para atender às diferentes necessidades de consulta, minimizando assim a necessidade de __junções complexas__.

4. Consultas orientadas por acesso:
* A __modelagem de dados__ no Cassandra é __orientada pelas consultas__ que serão executadas no sistema. Isso significa que o __esquema de dados__ deve ser __projetado__ em __torno das consultas__ que serão __feitas__ com __mais frequência__.
* As tabelas podem ser __criadas com base nas consultas__ para __otimizar__ o __acesso aos dados__ e __garantir__ que as __consultas__ sejam __eficientes__.

5. Tamanho de partição e anti-patterns:
* É importante evitar partições muito grandes, pois isso pode levar a problemas de desempenho e escalabilidade. Partições grandes podem resultar em nós sobrecarregados e consultas lentas.
* Da mesma forma, partições muito pequenas também devem ser evitadas, pois podem resultar em muitas partições pequenas sendo distribuídas no cluster, o que pode afetar negativamente o desempenho.

A __modelagem de dados__ no Apache Cassandra requer uma __abordagem diferente__ da utilizada em bancos de dados relacionais. É essencial __projetar o esquema__ de dados com base nas __necessidades específicas de consulta__ e nas __características de escalabilidade e distribuição__ do Cassandra. O objetivo é obter um __desempenho otimizado__ e garantir que o sistema possa crescer e se adaptar às demandas crescentes de dados.

### Algumas dicas e exemplos na prática sobre a modelagem de dados no Apache Cassandra:

__Dica__: Antes de construir sua tabela no Cassandra pense primeiro com bastante carinho em quem vai consumir esse dado. Isso é extremamente importante pois, como já mencionei anteriormente a tabela é construída para atender uma consulta especifica. Se você tiver outras necessidades (i.e., uma segunda consulta que deve responder outra pergunta com os dados) sobre os mesmos dados pode ser que seja necessário duplicar os dados dessa primeira tabela para uma segunda tabela que tenha uma estrutura de armazenamento (DDL) com caracteristicas distintas da primeira tabela mas que possuem os mesmos atributos.

__Um pouco de conceito e prática__:

No Cassandra você guarda suas tabelas em __Keyspaces__.

1.  Criação do Keyspace:

Um __Keyspace no Cassandra__ é __equivalente__ a um __banco de dados__ em __sistemas__ de gerenciamento de banco de dados __relacionais__ (RDBMS). É o espaço que contém tabelas relacionadas. Para criar um Keyspace, você pode usar a linguagem CQL (Cassandra Query Language).

Outro ponto importante relacionado ao Keyspace é a estratégia de replicação dos dados. 
No Apache Cassandra, a estratégia de replicação é um aspecto crucial para garantir a disponibilidade e a confiabilidade dos dados em um cluster distribuído. A estratégia de replicação determina como os dados são replicados entre os nós do cluster para garantir a tolerância a falhas e a recuperação de desastres. Existem duas estratégias principais de replicação no Cassandra: "__SimpleStrategy__" e "__NetworkTopologyStrategy__".

* __SimpleStrategy__:
A estratégia "SimpleStrategy" é usada quando o cluster Cassandra está em um único datacenter. Nessa abordagem, a replicação é feita de forma síncrona para os nós subsequentes no anel de partições.
Exemplo de "SimpleStrategy":

```sql
CREATE KEYSPACE nome_keyspace
WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
```

Neste exemplo, a estratégia de replicação "SimpleStrategy" está definida para um fator de replicação de 3. Isso significa que cada partição será replicada em três nós diferentes no mesmo datacenter.

Obs: para garantir uma alta disponibilidade minima o valor minimo recomendado de replicação dentro de um keyspace é 3.

* __NetworkTopologyStrategy__:
A estratégia "NetworkTopologyStrategy" é usada quando o cluster Cassandra se estende por vários datacenters. Ela permite que você controle a replicação entre os datacenters de forma mais granular, tornando-a adequada para ambientes distribuídos com várias regiões geográficas.
Exemplo de "NetworkTopologyStrategy":

```sql
CREATE KEYSPACE my_keyspace
WITH replication = {
    'class': 'NetworkTopologyStrategy',
    'datacenter1': 3,
    'datacenter2': 2
};
```
Neste exemplo, a estratégia de replicação "NetworkTopologyStrategy" está definida para replicar os dados em dois datacenters: "datacenter1" e "datacenter2". O fator de replicação é definido como 3 para "datacenter1" e 2 para "datacenter2". Isso significa que cada partição será replicada em três nós no "datacenter1" e em dois nós no "datacenter2".

As estratégias de replicação permitem que você controle como os dados são distribuídos e replicados em todo o cluster Cassandra. É importante escolher a estratégia adequada com base na topologia do seu cluster, nos requisitos de disponibilidade, na consistência dos dados e na resiliência a falhas. O Cassandra oferece flexibilidade para personalizar as estratégias de replicação de acordo com as necessidades específicas do seu ambiente distribuído.

__Um pouco sobre as chaves primária e de partição__:

No Apache Cassandra, o conceito de chave primária é fundamental para determinar como os dados são organizados, distribuídos e acessados em uma tabela. A chave primária é composta pela combinação de duas partes: a chave de partição (partition key) e a chave de clustering (clustering key). Vamos entender cada uma delas com exemplos.


__Chave Primária (Primary Key)__:

* A chave primária é usada para identificar exclusivamente um registro em uma tabela. Ela pode ser composta por uma ou mais colunas.
* Se a chave primária for composta por mais de uma coluna, a combinação dessas colunas deve ser única para cada registro na tabela.
* Cada tabela no Cassandra __deve ter__ uma __chave primária definida__.

__Chave de Partição (Partition Key)__:

* A chave de partição é a primeira parte da chave primária e é usada para determinar em qual partição (nó) os dados serão armazenados.
* A chave de partição é responsável pelo particionamento dos dados em todo o cluster. Cada partição representa uma unidade de armazenamento distribuída.
* Os dados dentro de uma partição são armazenados em ordem de acordo com a chave de clustering (se houver).
* A escolha da chave de partição é crítica, pois ela determina como os dados são distribuídos entre os nós e pode afetar o desempenho e a escalabilidade do sistema.

__Chave de Clustering (Clustering Key)__:

* A chave de clustering é a segunda parte da chave primária (se houver) e é usada para determinar a ordenação dos dados dentro de uma partição.
* Se uma tabela tiver apenas uma coluna na chave primária (chave de partição), ela será distribuída em partições separadas e não haverá ordenação dentro dessas partições.
* No entanto, se a chave primária contiver mais de uma coluna (incluindo a chave de partição), as colunas adicionais serão a chave de clustering e definirão a ordenação dos dados dentro da partição.

__Obs__: Antes de criar uma tabela lembre-se de estar dentro do seu Keyspace. Essa etapa é bem semelhante quando você deseja utilizar algum banco de dados relacional. Exemplo:
```sql
USE "nome_Keyspace" ;
```

Exemplo:
Vamos criar um exemplo de tabela no Cassandra para entender a chave primária, a chave de partição e a chave de clustering na prática.

Criação da Tabela:
```sql
CREATE TABLE products (
    category TEXT,
    product_id UUID,
    name TEXT,
    price DECIMAL,
    PRIMARY KEY (category, product_id)
);

```

Neste exemplo, estamos criando uma tabela chamada "products" com quatro colunas: "category", "product_id", "name" e "price".

* A __chave primária__ desta tabela é __composta__ pelas __colunas__ "__category__" e "__product_id__".
* A coluna "__category__" é a __chave de partição__, que __determina__ em qual __partição__ os dados serão __armazenados__.
* A coluna "__product_id__" é a __chave de clustering__, que __determina__ a __ordenação__ dos dados __dentro de cada partição__.

__Populando nossa tabela com um exemplo__:

Inserção de Dados:
```sql
INSERT INTO products (category, product_id, name, price)
VALUES ('electronics', uuid(), 'Smartphone', 699.99);

INSERT INTO products (category, product_id, name, price)
VALUES ('electronics', uuid(), 'Tablet', 399.99);

INSERT INTO products (category, product_id, name, price)
VALUES ('clothing', uuid(), 'T-Shirt', 29.99);

```

Neste exemplo, estamos inserindo três produtos na tabela "products" para diferentes categorias.

Entendendo a Chave Primária e Particionamento:

* Suponha que o Cassandra tenha um cluster com três nós e que o hashing da chave de partição resulte nos seguintes valores:

```shell
HASH('electronics') -> Partição 1 -> Nó 1
HASH('clothing')    -> Partição 2 -> Nó 2
```

* Os dados dos produtos de eletrônicos (category='electronics') são armazenados na Partição 1 no Nó 1, e os dados dos produtos de roupas (category='clothing') são armazenados na Partição 2 no Nó 2.

__Entendendo a Chave de Clustering e Ordenação__:

* Dentro de cada partição, os dados são ordenados com base no valor da chave de clustering (product_id).
* Os dados dentro da Partição 1 (category='electronics') são ordenados de acordo com os valores de "product_id", e o mesmo ocorre para a Partição 2 (category='clothing').

A chave primária, a chave de partição e a chave de clustering no Apache Cassandra são conceitos importantes para projetar o esquema de dados de forma eficiente e garantir um bom desempenho no acesso aos dados. A escolha adequada das chaves de partição e clustering é essencial para uma distribuição uniforme dos dados em todo o cluster e uma organização eficiente dentro de cada partição.

__Dica__: Imagine que você necessite que o seu dado já venha ordenado quando você faz uma consulta sem precisar explicitar isso sabendo que o retornado sempre precisará estar ordenado. Imaginou??? Bom vamos lá então:

O "__CLUSTERING ORDER BY__" no Apache Cassandra é usado para __definir a ordenação__ dos dados __dentro de uma partição__ com base em __uma ou mais__ colunas da __chave de clustering__. Isso permite que você especifique a ordem em que as linhas devem ser armazenadas em cada partição. Vamos utilizar o exemplo anterior da tabela "products" e adicionar a cláusula "CLUSTERING ORDER BY" para entender como funciona.


Criação da Tabela anteior com CLUSTERING ORDER BY:
```sql
CREATE TABLE products (
    category TEXT,
    product_id UUID,
    name TEXT,
    price DECIMAL,
    PRIMARY KEY (category, product_id)
) WITH CLUSTERING ORDER BY (product_id DESC);

```

Neste exemplo, estamos criando a mesma tabela "products", mas adicionamos a cláusula "WITH CLUSTERING ORDER BY (product_id DESC)" na definição da tabela.

A cláusula "WITH CLUSTERING ORDER BY" especifica que os dados dentro de cada partição serão ordenados pelo valor da coluna "product_id" em ordem decrescente (DESC). Isso significa que os produtos dentro de cada categoria serão armazenados em ordem decrescente com base no ID do produto.

Vamos inserir mais alguns dados...
Inserção de Dados:
```sql
INSERT INTO products (category, product_id, name, price)
VALUES ('electronics', uuid(), 'Smartphone A', 599.99);

INSERT INTO products (category, product_id, name, price)
VALUES ('electronics', uuid(), 'Smartphone B', 699.99);

INSERT INTO products (category, product_id, name, price)
VALUES ('electronics', uuid(), 'Smartphone C', 799.99);

```

Neste exemplo, estamos inserindo três produtos de eletrônicos na tabela "products" com diferentes valores de "product_id".

__Entendendo o CLUSTERING ORDER BY__:

Suponha que o Cassandra tenha um cluster com três nós e que o hashing da chave de partição resulte nos seguintes valores:

```shell
HASH('electronics') -> Partição 1 -> Nó 1
```

Os dados dos produtos de eletrônicos (category='electronics') são armazenados na Partição 1 no Nó 1 assim como nos exemplos anteriores.

__Ordenação dentro da Partição__:

* Os dados dentro da Partição 1 (category='electronics') são ordenados com base no valor da coluna "product_id" em ordem decrescente.

* Isso significa que os produtos serão armazenados na seguinte ordem dentro da Partição 1:
```shell
'Smartphone C', product_id = UUID3
'Smartphone B', product_id = UUID2
'Smartphone A', product_id = UUID1
```

* Observe que os dados são ordenados de acordo com o valor do "product_id" em ordem decrescente.

O "__CLUSTERING ORDER BY__" é útil quando você precisa recuperar os dados em uma ordem específica com base nos valores das colunas de clustering. A ordenação pode ser ascendente (ASC) ou decrescente (DESC), permitindo que você controle a organização dos dados dentro de cada partição. É importante escolher a coluna certa para a ordenação com base nos requisitos do seu aplicativo para otimizar as consultas.

Boa sorte nos seus estudos! Eu espero ter te ajudado mesmo que somente um pouquinho na sua jornada.