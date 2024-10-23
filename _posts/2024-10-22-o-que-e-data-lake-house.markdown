---
layout: post
title:  "O que é Data LakeHouse?"
date:   2024-10-22 00:00:00 -0300
categories: data data-analytics data-architecture arquitetura-de-dados data-lake-house lakehouse lake-house analytics
---

![Data LakeHouse]({{ site.url }}/assets/arquitetura-data-lake-house.png){:style="width: 100%" }

Fala pessoal blz? Nesse post vou ensinar para vocês o conceito de arquitetura __Data Lakehouse__.

Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

**Data Lakehouse** é uma arquitetura moderna de armazenamento de dados que combina as melhores características de dois modelos tradicionais: o [**Data Lake**]({% post_url 2024-08-25-o-que-e-data-lake %}){:target="_blank"}  e o [**Data Warehouse**]({% post_url 2024-07-30-o-que-e-data-warehouse %}){:target="_blank"}. Ele visa resolver algumas das limitações que esses modelos apresentam individualmente, oferecendo uma solução mais flexível e eficiente para grandes volumes de dados.

### Entendendo o Data Lake e o Data Warehouse

1. **Data Lake**:
   - Um **Data Lake** é um repositório centralizado onde os dados são armazenados em seu formato bruto (não processado), seja ele estruturado (como tabelas), semiestruturado (como arquivos JSON ou XML) ou não estruturado (como arquivos de áudio e vídeo).
   - Geralmente utiliza armazenamento de baixo custo, como sistemas de arquivos distribuídos (por exemplo, **HDFS** ou **Amazon S3**).
   - Embora permita armazenar grandes volumes de dados com facilidade, um Data Lake carece de mecanismos sofisticados de gerenciamento de dados, como controle de qualidade, segurança e governança, o que pode levar a problemas de consistência e performance.

2. **Data Warehouse**:
   - Um **Data Warehouse**, por outro lado, é um sistema projetado especificamente para armazenar e processar grandes volumes de dados estruturados, geralmente provenientes de diferentes fontes, em um formato já processado e otimizado para análises.
   - O foco está em **consultas rápidas** e **relatórios eficientes**. No entanto, os Data Warehouses são caros de manter, menos flexíveis e, geralmente, não lidam bem com dados semiestruturados ou não estruturados.

### O Que é uma Data Lakehouse?

**Data Lakehouse** é uma arquitetura que visa unir as vantagens do Data Lake (armazenamento econômico e flexível para todos os tipos de dados) com as vantagens do Data Warehouse (alta performance, governança, e capacidade analítica robusta). Isso é feito com base em três pilares:

1. **Armazenamento unificado**:
   - O Data Lakehouse permite armazenar todos os tipos de dados (estruturados, semiestruturados e não estruturados) no mesmo sistema, usando o formato bruto do **Data Lake**.
   - Em vez de separar os dados em diferentes silos (um para dados não estruturados e outro para dados estruturados), todos os dados são armazenados de maneira integrada e acessível.

2. **Suporte para análise transacional e analítica**:
   - Como um Data Warehouse, o Data Lakehouse suporta **transações ACID** (Atomicidade, Consistência, Isolamento e Durabilidade), o que significa que ele pode lidar com atualizações e consultas simultâneas de forma confiável.
   - Ele é otimizado para realizar **consultas rápidas e eficientes** sobre grandes volumes de dados, assim como um Data Warehouse. Isso é conseguido utilizando **camadas de otimização** no processamento de dados, como **Delta Lake** ou **Apache Iceberg**.

3. **Governança e qualidade de dados**:
   - O Data Lakehouse melhora a governança e a qualidade dos dados em relação ao Data Lake, oferecendo funcionalidades de auditoria, controle de versão e segurança granular. Assim, ele pode manter a qualidade dos dados e proporcionar um ambiente seguro e rastreável para análise.

### Benefícios do Data Lakehouse

- **Redução de custos**: Ao usar armazenamento de baixo custo (como em um Data Lake), mas com a capacidade de processamento e otimização de um Data Warehouse, o Data Lakehouse oferece um modelo de armazenamento mais econômico.
  
- **Flexibilidade**: Como o Data Lakehouse pode armazenar dados estruturados, semiestruturados e não estruturados em um único repositório, ele é muito mais flexível e adequado para cenários de Big Data.

- **Análise unificada**: Com a capacidade de processar dados em tempo real e dados históricos, ele é ideal para análises avançadas, como machine learning e BI (Business Intelligence), sem precisar mover os dados entre sistemas separados.

- **Escalabilidade**: Assim como um Data Lake, ele pode lidar com quantidades massivas de dados, mas sem as limitações de performance que um Data Lake puro pode ter.

### Exemplos de Implementações de Data Lakehouse

- **Delta Lake**: Um dos primeiros frameworks a popularizar o conceito de Data Lakehouse. Ele adiciona a capacidade de transações ACID e controle de versão sobre um Data Lake.
  
- **Apache Iceberg** e **Apache Hudi**: São tecnologias que fornecem funcionalidades similares, garantindo que os dados armazenados no formato bruto de um Data Lake possam ser lidos, atualizados e versionados com eficiência.

- **Google BigLake** e **AWS Lake Formation**: São exemplos de serviços na nuvem que oferecem plataformas Lakehouse como solução gerenciada.

### Conclusão referente ao conceito de arquitetura Data Lakehouse

O **Data Lakehouse** surge como uma solução moderna e eficaz para armazenar e processar grandes volumes de dados, unificando a flexibilidade e custo baixo de um Data Lake com a confiabilidade e capacidade analítica de um Data Warehouse. Ele é ideal para empresas que precisam lidar com diversos tipos de dados e realizar análises avançadas em escala, sem sacrificar performance, governança ou custo.

### Arquitetura de dados Data Lakehouse modelo Medallion

A **arquitetura de dados Medallion** (ou arquitetura de camadas) é uma abordagem de organização e processamento de dados, frequentemente usada no contexto de **Data Lakehouse**. O principal objetivo dessa arquitetura é melhorar a qualidade dos dados, organizar o fluxo de dados e garantir que o processo de transformação seja escalável e eficiente. A arquitetura de dados Medallion divide os dados em diferentes camadas, ou "níveis de qualidade", à medida que eles passam por processos de ingestão, limpeza e enriquecimento.

### Estrutura da Arquitetura Medallion

![Data LakeHouse]({{ site.url }}/assets/arquitetura-data-lake-house-medallion.png){:style="width: 100%" }

A arquitetura de dados Medallion é normalmente dividida em três camadas principais:

1. **Bronze Layer (Camada Bronze)** – **Dados Brutos**
   - Esta é a camada de **dados brutos**, onde os dados são armazenados logo após serem ingeridos no sistema, diretamente das fontes. Eles são armazenados no formato original, com pouca ou nenhuma modificação.
   - Os dados podem ser estruturados (bancos de dados relacionais), semiestruturados (JSON, XML) ou não estruturados (imagens, vídeos, logs).
   - Objetivo: Ter uma cópia fiel dos dados originais, o que garante rastreabilidade, e serve como backup caso haja necessidade de rever dados históricos.

2. **Silver Layer (Camada Prata)** – **Dados Refinados e Limpos**
   - Nesta camada, os dados passam por um processo de **limpeza, deduplicação e filtragem**. Os dados "sujos" e inconsistentes são corrigidos, ou pelo menos marcados, e o que sobra são dados mais organizados e confiáveis.
   - É também aqui que ocorrem **junções e agregações iniciais** entre diferentes fontes de dados, preparando-os para análises mais detalhadas.
   - Objetivo: Oferecer uma versão de dados "limpa", onde análises e relatórios possam ser realizados com maior confiança nos resultados.

3. **Gold Layer (Camada Ouro)** – **Dados Prontos para Consumo**
   - Na camada Gold, os dados estão no formato final, altamente **agregados e enriquecidos**, prontos para serem usados diretamente em **relatórios**, **painéis de BI** (Business Intelligence) e **modelos de machine learning**.
   - Os dados nesta camada são organizados de acordo com as necessidades de negócios, geralmente otimizados para consultas rápidas e de alto desempenho.
   - Objetivo: Fornecer dados prontos para consumo pelos usuários finais ou por sistemas de análise avançada, com total confiabilidade e performance.

### Benefícios da Arquitetura Medallion

- **Escalabilidade**: O fluxo de dados é organizado em etapas, o que permite que o sistema escale conforme o volume de dados aumenta.
- **Rastreabilidade e controle de versão**: As diferentes camadas mantêm versões intermediárias dos dados (bronze e prata), o que permite rastrear as transformações que os dados sofreram.
- **Flexibilidade**: Novas fontes de dados podem ser adicionadas à camada Bronze sem interromper as camadas superiores, oferecendo flexibilidade para ingestão de dados em diferentes formatos e frequências.
- **Governança de Dados**: Com os dados sendo processados de forma incremental, é mais fácil implementar políticas de governança e controle de qualidade de dados.

### Relação com a Arquitetura **Data Lakehouse**

A **arquitetura Medallion** é frequentemente usada dentro de um **Data Lakehouse**, já que ela complementa o modelo de organização de dados necessário para manter um repositório unificado de dados de diferentes tipos e qualidades.

- **Data Lakehouse** combina os benefícios de um **Data Lake** (armazenamento bruto e flexível) com um **Data Warehouse** (alta performance e controle sobre dados), e a arquitetura Medallion desempenha um papel central em **gerenciar a qualidade** e **preparar** esses dados em diferentes fases de processamento.
  
- No **Data Lakehouse**, os dados são geralmente armazenados em um **Data Lake** na camada Bronze, processados e refinados nas camadas Prata e Ouro, garantindo que os dados que chegam aos usuários finais ou sistemas de análise estejam no formato ideal, com alta qualidade e performance.

- A arquitetura Medallion **resolve o problema da qualidade de dados** que os **Data Lakes** tradicionais enfrentavam (onde dados brutos eram frequentemente difíceis de usar diretamente). Ao passar por essas camadas, os dados são gradualmente refinados e organizados, permitindo que o Data Lakehouse aproveite o melhor dos dois mundos: o baixo custo de armazenamento de dados brutos e a eficiência de um Data Warehouse para consultas.

### Exemplo de Fluxo Medallion em um Data Lakehouse

1. **Ingestão de Dados (Camada Bronze)**: Suponha que você tenha dados de sensores IoT, logs de transações e dados de clientes. Esses dados são inicialmente armazenados na camada Bronze, sem qualquer modificação, para preservar sua integridade original.
   
2. **Processamento Inicial (Camada Prata)**: Os dados de logs podem ser processados para remover erros, duplicatas ou ruídos. Os dados de sensores podem ser filtrados e combinados com os dados de transações.

3. **Dados Prontos para Consumo (Camada Ouro)**: Finalmente, esses dados refinados são preparados e agregados, prontos para uso em análises de negócios, como análise de comportamento de clientes, predição de falhas de dispositivos ou otimização de processos de vendas.

### Conclusão referente ao conceito de arquitetura Medallion

A **arquitetura Medallion** organiza o processamento de dados em camadas, facilitando a escalabilidade, a governança e a qualidade dos dados dentro de um **Data Lakehouse**. Ela ajuda a garantir que os dados sejam refinados e preparados de forma eficiente, permitindo que os benefícios do Data Lake (armazenamento barato e flexível) e do Data Warehouse (dados prontos para análise com alta performance) sejam totalmente aproveitados.

**Links de referência** de outras fontes para mais aprofundamento nos assuntos discutidos nesse post:
* [Arquitetura Medallion](https://www.databricks.com/br/glossary/medallion-architecture#:~:text=A%20arquitetura%20medallion%20se%20refere,Bronze%20%E2%87%92%20Prata%20%E2%87%92%20Ouro){:target="_blank"};
* [Data LakeHouse](https://www.databricks.com/br/glossary/data-lakehouse){:target="_blank"};
* [Delta Lake](https://delta.io/){:target="_blank"};
* [Apache Iceberg](https://iceberg.apache.org/){:target="_blank"};
* [Apache Hudi](https://hudi.apache.org/){:target="_blank"};
* [Apache Xtable](https://xtable.incubator.apache.org/){:target="_blank"} esse aqui vou acrescentar de brinde. Esse é uma ferramenta que facilita a operacionalização entre (Delta Lake, Apache Hudi e Iceberg) para o caso de você precisar fazer esses queridos conversarem entre si.

Em futuros posts vou trazer exemplos de uso dessas ferramentas para vocês implementarem e sentirem na prática como elas funcionam e se comportam.