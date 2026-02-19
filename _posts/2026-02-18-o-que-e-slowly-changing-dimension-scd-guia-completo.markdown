--- 
layout: post
title:  "Como Gerenciar Histórico de Dados: Tudo sobre SCD com Exemplos Práticos"
date:   2026-02-18 09:00:00 -0300
categories: scd data dados bigdata bi warehouse
---

![SCD]({{ site.url }}/assets/scd.png){:style="width: 100%" }

# SCD (Slowly Changing Dimension): Guia Completo do Básico ao Avançado em Data Warehouses e Lakehouses

Se você trabalha com **Engenharia de Dados, BI ou Arquitetura de Dados**, em algum momento já se deparou com esta pergunta:

> Como preservar a verdade histórica dos dados quando eles mudam ao longo do tempo?

Essa é exatamente a motivação por trás do **SCD (Slowly Changing Dimension)**.

Neste artigo você vai entender:

* O que é SCD
* Por que ele é essencial em Data Warehouses
* Todos os principais tipos (0 a 7)
* Quando usar cada abordagem
* Como isso se conecta com arquiteturas modernas de Lakehouse


# O que é SCD (Slowly Changing Dimension)?

**SCD (Slowly Changing Dimension)** é uma técnica de modelagem dimensional usada para tratar mudanças em atributos de tabelas dimensão ao longo do tempo.

Em um modelo analítico tradicional temos:

* **Tabelas Fato** → armazenam eventos (vendas, transações, cliques)
* **Tabelas Dimensão** → armazenam atributos descritivos (cliente, produto, região)

O problema surge quando atributos da dimensão mudam.

Exemplo:

| id_cliente | nome | cidade    |
| ---------- | ---- | --------- |
| 10         | Ana  | São Paulo |

Se Ana muda para Campinas, você deve:

* Atualizar o registro?
* Manter histórico?
* Criar nova linha?

A resposta depende da estratégia de SCD adotada.


# Por que SCD é tão importante?

Sem SCD, análises históricas ficam incorretas.

Pergunta clássica:

> Quanto vendemos quando nossos clientes moravam em São Paulo?

Se você sobrescrever os dados, essa resposta se perde.

SCD garante:

* Análises temporais corretas
* Conformidade regulatória
* Rastreamento de evolução de clientes
* Consistência analítica

SCD não é apenas uma técnica de banco.
É um mecanismo de preservação da verdade histórica.

# Tipos Clássicos de SCD

## 🔹 SCD Tipo 0 — Não altera

Mudanças são ignoradas.

Uso:

* Data de nascimento
* CPF
* Dados imutáveis

✔ Simples
❌ Não permite atualização


## 🔹 SCD Tipo 1 — Sobrescreve

Substitui o valor antigo.

Antes:
| 10 | Ana | São Paulo |

Depois:
| 10 | Ana | Campinas |

✔ Simples
❌ Histórico perdido

Indicado para:

* Correções de erro
* Dados irrelevantes historicamente

## 🔹 SCD Tipo 2 — Histórico Completo (o mais utilizado)

Cada mudança gera uma nova linha.

| sk | id_cliente | cidade    | dt_inicio  | dt_fim     | ativo |
| -- | ---------- | --------- | ---------- | ---------- | ----- |
| 1  | 10         | São Paulo | 2023-01-01 | 2024-01-10 | N     |
| 2  | 10         | Campinas  | 2024-01-10 | NULL       | S     |

✔ Histórico completo
✔ Permite análises temporais detalhadas
❌ Tabela cresce com o tempo

Este é o padrão dominante em Data Warehouses corporativos.

## 🔹 SCD Tipo 3 — Histórico limitado

Mantém apenas o valor anterior.

| id | cidade_atual | cidade_anterior |
| -- | ------------ | --------------- |
| 10 | Campinas     | São Paulo       |

✔ Simples
❌ Histórico restrito

# Tipos Avançados e Híbridos

Em ambientes mais maduros, surgem variações.

## 🔹 SCD Tipo 4 — Histórico Separado

* Tabela principal mantém apenas o estado atual
* Histórico fica em tabela separada

✔ Performance melhor para consultas atuais
✔ Histórico isolado
❌ Maior complexidade

## 🔹 SCD Tipo 5 — Tipo 1 + Tipo 4

Combinação de:

* Sobrescrita na dimensão principal
* Histórico mantido em tabela separada

Muito usado quando há exigência regulatória.

## 🔹 SCD Tipo 6 — Híbrido (1 + 2 + 3)

Combina múltiplas estratégias.

✔ Histórico completo
✔ Acesso rápido ao valor atual
✔ Acesso ao valor anterior
❌ Maior complexidade de modelagem

Comum em ambientes baseados em Kimball.

 🚀 Evolução dos dados na prática

## 🟢 Estado inicial (2023-01-01)

Carlos mora em São Paulo.

| sk_cliente | id_cliente | nome         | cidade_atual | cidade_anterior | dt_inicio  | dt_fim | ativo |
| ---------- | ---------- | ------------ | ------------ | --------------- | ---------- | ------ | ----- |
| 1          | 100        | Carlos Silva | São Paulo    | NULL            | 2023-01-01 | NULL   | S     |

## 🔵 Primeira mudança (2024-03-10)

Carlos muda para Rio de Janeiro.

O que acontece?

1. Linha anterior é encerrada
2. Nova linha é criada
3. cidade_anterior é preenchida
4. cidade_atual reflete novo valor

| sk_cliente | id_cliente | nome         | cidade_atual   | cidade_anterior | dt_inicio  | dt_fim     | ativo |
| ---------- | ---------- | ------------ | -------------- | --------------- | ---------- | ---------- | ----- |
| 1          | 100        | Carlos Silva | São Paulo      | NULL            | 2023-01-01 | 2024-03-10 | N     |
| 2          | 100        | Carlos Silva | Rio de Janeiro | São Paulo       | 2024-03-10 | NULL       | S     |

## 🟣 Segunda mudança (2025-02-01)

Carlos muda para Belo Horizonte.

| sk_cliente | id_cliente | nome         | cidade_atual   | cidade_anterior | dt_inicio  | dt_fim     | ativo |
| ---------- | ---------- | ------------ | -------------- | --------------- | ---------- | ---------- | ----- |
| 1          | 100        | Carlos Silva | São Paulo      | NULL            | 2023-01-01 | 2024-03-10 | N     |
| 2          | 100        | Carlos Silva | Rio de Janeiro | São Paulo       | 2024-03-10 | 2025-02-01 | N     |
| 3          | 100        | Carlos Silva | Belo Horizonte | Rio de Janeiro  | 2025-02-01 | NULL       | S     |

# 🔍 O que isso permite na prática?

### ✅ Histórico completo (Tipo 2)

Podemos saber onde ele morava em qualquer data.

### ✅ Valor anterior explícito (Tipo 3)

Sabemos imediatamente a cidade anterior sem precisar consultar linha anterior.

### ✅ Estado atual simplificado (Tipo 1)

A linha com `ativo = S` sempre contém o estado vigente.

# 📈 Por que isso é poderoso?

Você pode responder:

* Quanto vendemos quando ele morava no Rio?
* Qual foi a cidade anterior antes da atual?
* Qual é o estado atual sem fazer subquery?

# 🧠 Diferença visual rápida

| Tipo   | Histórico Completo | Guarda valor anterior | Sobrescreve atual |
| ------ | ------------------ | --------------------- | ----------------- |
| Tipo 2 | ✔                  | ❌                     | ❌                 |
| Tipo 3 | ❌                  | ✔                     | ✔                 |
| Tipo 6 | ✔                  | ✔                     | ✔                 |


## 🔹 SCD Tipo 7 — Dual Key

Mantém:

* Surrogate Key (SK): chave artificial usada pelo ambiente analítico para garanti unicidade entre os registros
* Natural Key (NK): chave primária do sistema de origem do dado

Permite consultas tanto por estado atual quanto histórico.

Exemplo prático no SCD tipo 6.

# SCD no Mundo Lakehouse Moderno

Com tecnologias como:

* Delta Lake
* Apache Iceberg
* Snowflake
* BigQuery
* Databricks

Temos:

* `MERGE INTO`
* Time Travel
* Snapshots
* Change Data Feed
* Versionamento automático

Isso muda a implementação…

Mas não elimina o problema conceitual.

Mesmo com versionamento nativo, você ainda precisa decidir:

* Quer manter múltiplas versões ativas?
* Quer sobrescrever?
* Quer histórico separado?

SCD continua sendo uma decisão arquitetural.

# Quando usar cada tipo?

| Cenário                       | Estratégia recomendada |
| ----------------------------- | ---------------------- |
| Correção de erro              | Tipo 1                 |
| Análise histórica completa    | Tipo 2                 |
| Histórico curto               | Tipo 3                 |
| Performance para estado atual | Tipo 4                 |
| Compliance + performance      | Tipo 5                 |
| BI corporativo complexo       | Tipo 6                 |

# Minha visão prática como arquiteto de dados

Ao longo da minha experiência em Engenharia e Arquitetura de Dados, vejo que:

* A maioria dos problemas analíticos mal resolvidos vem da falta de estratégia de SCD.
* Muitas equipes subestimam o impacto da sobrescrita de dados.
* Em ambientes Lakehouse, há uma falsa sensação de que o Time Travel resolve tudo — mas ele não substitui modelagem adequada.

SCD não é apenas um conceito acadêmico.
É uma decisão estratégica de arquitetura.

# Conclusão

Se você quer construir uma plataforma de dados robusta, escalável e analiticamente correta, dominar SCD é obrigatório.

Independentemente da tecnologia utilizada, o problema da mudança ao longo do tempo sempre existirá — e sempre exigirá estratégia.