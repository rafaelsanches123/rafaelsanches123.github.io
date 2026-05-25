--- 
layout: post
title:  "Kafka Connect, Debezium e CDC: Como Funcionam Juntos em Arquiteturas Orientadas a Eventos"
date:   2026-04-06 10:00:00 -0300
categories: cdc change-data-capture kafka-connect debezium replicação-de-dados nrt
---

![CDC]({{ site.url }}/assets/kafka-connect-cdc.png){:style="width: 100%" }

Arquiteturas modernas de dados exigem integração contínua, baixa latência e alta escalabilidade. Nesse contexto, três conceitos se destacam:

* **Change Data Capture (CDC)**
* **Kafka Connect**
* **Debezium**

Neste artigo, vamos entender como esses três elementos se relacionam e como são utilizados em arquiteturas modernas baseadas no Apache Kafka.


# 📌 O que é Change Data Capture (CDC)?

**CDC (Change Data Capture)** é uma estratégia para capturar alterações realizadas em um banco de dados — INSERT, UPDATE e DELETE — sem precisar reprocessar toda a base.

Em vez de fazer cargas completas (full load), o CDC captura apenas o que mudou.

Isso possibilita:

* Processamento incremental
* Redução de custo
* Integração quase em tempo real
* Arquiteturas orientadas a eventos

# 🔌 O que é Kafka Connect?

O **Kafka Connect** é um framework do ecossistema Kafka criado para integrar sistemas externos ao Kafka de forma:

* Padronizada
* Escalável
* Resiliente
* Sem necessidade de código customizado

Ele permite conectar:

* Bancos de dados
* Data Lakes
* APIs
* Sistemas legados
* Ferramentas SaaS

## 🧱 Tipos de Connectors

O Kafka Connect trabalha com dois tipos principais:

### 1️⃣ Source Connector

Leva dados **para dentro do Kafka**

Exemplo:
* Banco → Kafka

### 2️⃣ Sink Connector

Leva dados **do Kafka para fora**

Exemplo:
* Kafka → Data Lake
* Kafka → Elasticsearch
* Kafka → Banco de dados

# 🔍 Onde entra o Debezium?

O **Debezium** é um conjunto de **Source Connectors especializados em CDC**.

Ele roda **sobre o Kafka Connect**.

Ou seja:

```
Kafka Connect = Framework de Integração
Debezium = Plugin de CDC
```

O Debezium lê o log transacional do banco e publica eventos no Kafka.

Exemplo de logs:

* WAL no PostgreSQL
* Binlog no MySQL

# 🏗 Arquitetura Completa

Uma arquitetura típica com CDC moderno funciona assim:

```
Banco de Dados (PostgreSQL)
        ↓ (WAL)
Debezium (Source Connector)
        ↓
Kafka Connect (Distributed Mode)
        ↓
Apache Kafka (Tópicos)
        ↓
---------------------------------
↓                ↓               ↓
Spark       Microservices     Sink Connector
                                  ↓
                           Data Lake / Lakehouse
```

# ⚙️ Funcionamento Interno

## 1️⃣ Banco gera log transacional

Cada alteração é registrada no log (WAL, Binlog etc.)

## 2️⃣ Debezium lê o log

Transforma alterações em eventos estruturados.

## 3️⃣ Kafka Connect gerencia o conector

* Armazena offsets
* Controla paralelismo
* Gerencia falhas
* Permite escala horizontal

## 4️⃣ Kafka distribui eventos

Os eventos são publicados em tópicos.

## 5️⃣ Consumidores processam

* Spark Structured Streaming
* Flink
* Microservices
* Sink Connectors

# 📦 Exemplo de Evento CDC Publicado

```json
{
  "before": {
    "id": 10,
    "nome": "Rafael"
  },
  "after": {
    "id": 10,
    "nome": "Rafael Sanches"
  },
  "op": "u",
  "ts_ms": 1708700000000
}
```

Esse modelo permite:

* SCD Tipo 2 orientado a eventos
* Atualização incremental em Lakehouse
* Event Sourcing
* CQRS

# 🔥 Por que essa arquitetura é poderosa?

Porque ela:

* Elimina full loads
* Reduz latência
* Permite escalabilidade horizontal
* Desacopla sistemas
* Facilita Data Products no Data Mesh
* Habilita processamento em streaming

# 🧠 Kafka Connect em Modo Distribuído

Em produção, o Kafka Connect roda em **Distributed Mode**:

* Vários workers
* Rebalanceamento automático
* Alta disponibilidade
* REST API para gerenciamento

Isso transforma integração de dados em um serviço escalável.

# 📊 Comparação Conceitual

| Camada        | Responsabilidade                |
| ------------- | ------------------------------- |
| CDC           | Estratégia de capturar mudanças |
| Debezium      | Implementação de CDC            |
| Kafka Connect | Infraestrutura de integração    |
| Kafka         | Distribuição de eventos         |
| Consumers     | Processamento e persistência    |


# 🧩 Conexão com Lakehouse e Data Mesh

Essa arquitetura é essencial para:

* Lakehouse incremental
* Medallion Architecture
* Event-Driven Architecture
* Data Products orientados a domínio
* Governança federada
* Data Contracts

No contexto de Spark + Iceberg, por exemplo, é possível consumir eventos e aplicar MERGE INTO incrementalmente.

# 🚀 Conclusão

Kafka Connect e Debezium não substituem o CDC — **eles operacionalizam o CDC em escala**.

Se CDC é a estratégia,
Kafka Connect é a infraestrutura,
e Debezium é o motor.

Essa combinação é um dos pilares da engenharia de dados moderna.
