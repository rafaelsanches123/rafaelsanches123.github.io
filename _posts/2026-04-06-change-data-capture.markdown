--- 
layout: post
title:  "Change Data Capture (CDC): O que é, como funciona e por que é essencial em arquiteturas modernas de dados"
date:   2026-04-06 09:00:00 -0300
categories: cdc change-data-capture replicação-de-dados nrt
---

![CDC]({{ site.url }}/assets/cdc.png){:style="width: 100%" }

Em arquiteturas modernas orientadas a dados e eventos, processar apenas o que mudou é uma necessidade — não um luxo.

É aqui que entra o **Change Data Capture (CDC)**.

Neste artigo você vai entender:

* O que é CDC
* Como ele funciona
* Quais são as principais estratégias
* Como implementar na prática
* Como ele se conecta com Data Mesh, Lakehouse e Streaming
* Quando usar (e quando evitar)


# 📌 O que é Change Data Capture?

**Change Data Capture (CDC)** é uma técnica usada para identificar e capturar alterações realizadas em um banco de dados — como:

* INSERT
* UPDATE
* DELETE

Em vez de realizar cargas completas (full load), o CDC captura apenas as mudanças desde a última execução.

Isso reduz:

* Custo computacional
* Latência
* Impacto no banco transacional

E viabiliza arquiteturas quase em tempo real.


# 🎯 O problema que o CDC resolve

Imagine uma tabela com 50 milhões de registros.

Sem CDC, você teria duas opções:

1. Reprocessar tudo diariamente (alto custo)
2. Criar filtros manuais por data (arriscado e limitado)

O CDC resolve isso capturando alterações diretamente na origem — muitas vezes no próprio log transacional do banco.


# 🔎 Principais Estratégias de CDC

Existem três abordagens principais.


## 1️⃣ CDC baseado em Timestamp

A tabela possui campos como:

```sql
created_at
updated_at
```

Consulta incremental típica:

```sql
SELECT *
FROM clientes
WHERE updated_at > '2026-02-20 10:00:00'
```

### ✅ Vantagens

* Simples
* Fácil de implementar
* Baixa complexidade

### ❌ Desvantagens

* Não captura DELETE facilmente
* Depende de disciplina de modelagem
* Pode perder alterações


## 2️⃣ CDC baseado em Trigger

Aqui são criadas triggers para registrar alterações em uma tabela de auditoria.

```sql
CREATE TRIGGER clientes_update
AFTER UPDATE ON clientes
FOR EACH ROW
INSERT INTO clientes_log (...)
```

### ✅ Vantagens

* Captura INSERT, UPDATE e DELETE
* Controle total

### ❌ Desvantagens

* Impacta performance
* Aumenta acoplamento
* Complexidade operacional


## 3️⃣ CDC baseado em Log de Transações (Log-Based CDC) ⭐

Essa é a abordagem mais robusta e utilizada atualmente.

Ela lê diretamente o log de transações do banco:

* WAL no PostgreSQL
* Binlog no MySQL
* Redo Log no Oracle

Como as mudanças já são registradas no log do banco, o impacto na aplicação é mínimo.


# 🛠 Ferramentas Populares de CDC

Algumas das ferramentas mais utilizadas no mercado:

* Debezium
* Maxwell
* AWS Database Migration Service
* Azure Data Factory

Muitas delas publicam eventos em:

* Apache Kafka


# 🏗 Arquitetura Moderna com CDC

Uma arquitetura típica:

```
PostgreSQL
   ↓ (WAL)
Debezium
   ↓
Kafka
   ↓
Spark / Flink / Consumers
   ↓
Data Lake / Lakehouse
```

Isso permite:

* Atualizações quase em tempo real
* Replicação entre sistemas
* Construção de Data Products
* Atualização incremental em Lakehouse


# 📦 Exemplo de Evento CDC

Um evento típico emitido pelo Debezium:

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

Onde:

* `c` → create
* `u` → update
* `d` → delete
* `r` → snapshot

Esse modelo é ideal para processamento em streaming.


# 🧠 CDC e Arquiteturas Modernas

O CDC é peça-chave em:

* Lakehouse incremental
* Medallion Architecture
* Event-Driven Architecture
* CQRS
* Event Sourcing
* Data Mesh

Ele transforma o banco transacional em uma fonte de eventos.


# 🔄 CDC vs Batch Tradicional

| Critério       | Batch Full | CDC       |
| -------------- | ---------- | --------- |
| Latência       | Alta       | Baixa     |
| Custo          | Alto       | Otimizado |
| Tempo real     | Não        | Sim       |
| Escalabilidade | Limitada   | Alta      |
| Complexidade   | Baixa      | Média     |


# ⚠️ Desafios do CDC

Embora poderoso, CDC traz desafios:

* Ordenação de eventos
* Schema evolution
* Garantia de exactly-once
* Reprocessamento
* Compactação
* Tratamento de deletes
* LGPD / direito ao esquecimento

Em ambientes com Spark e Iceberg, por exemplo, é necessário tratar merges corretamente para evitar inconsistências.


# 🎓 Quando Usar CDC?

Use quando:

✔ Precisa de dados quase em tempo real

✔ Quer evitar full loads pesados

✔ Precisa sincronizar sistemas

✔ Está construindo arquitetura orientada a eventos

Evite quando:

❌ O volume é pequeno

❌ Atualizações são raras

❌ Complexidade não compensa


# 🚀 Conclusão

O **Change Data Capture** é uma das tecnologias mais importantes da engenharia de dados moderna.

Ele permite:

* Processamento incremental
* Arquiteturas escaláveis
* Baixa latência
* Integração orientada a eventos
* Construção de Data Products

Se você trabalha com Spark, Kafka, Lakehouse ou Data Mesh, dominar CDC deixa de ser opcional — torna-se essencial.