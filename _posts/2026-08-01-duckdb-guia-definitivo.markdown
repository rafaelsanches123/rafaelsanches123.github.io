--- 
layout: post
title: "DuckDB: O Guia Definitivo para Análise de Dados Moderna (Do Básico ao Avançado)"
date: 2026-08-01 10:00:00 -0300
categories: análise data analytics descritiva diagnóstica preditiva prescritiva cognitiva tempo real ciência dados business intelligence duckdb
---

![DuckDB]({{ site.url }}/assets/duckdb.png){:style="width: 100%" }

Imagine conseguir analisar milhões de registros em segundos utilizando apenas SQL, sem instalar um servidor de banco de dados, sem importar arquivos e consumindo pouca memória.

Parece bom demais para ser verdade?

Essa é exatamente a proposta do **DuckDB**.

Criado por pesquisadores da Universidade de Amsterdã (CWI) e do MIT, o DuckDB foi desenvolvido para resolver um problema muito comum: realizar análises analíticas (OLAP) de forma rápida, simples e eficiente diretamente na máquina do analista.

Nos últimos anos ele se tornou uma das ferramentas favoritas de Cientistas de Dados, Engenheiros de Dados e Analistas de BI, sendo integrado a projetos em Python, R, Polars, Pandas, Apache Arrow, Jupyter e Data Lakes baseados em Parquet.

Neste guia você aprenderá desde os primeiros comandos até recursos avançados utilizados em projetos reais.



# O que torna o DuckDB tão especial?

O DuckDB foi projetado especificamente para consultas analíticas.

Enquanto bancos transacionais, como PostgreSQL e MySQL, são excelentes para registrar operações do dia a dia, o DuckDB foi otimizado para responder perguntas sobre grandes volumes de dados.

Entre seus diferenciais estão:

* Não precisa de servidor dedicado.
* Funciona como uma biblioteca embarcada (*embedded*).
* Armazenamento colunar e execução vetorizada.
* Paralelismo automático.
* Leitura direta de CSV, JSON e Parquet.
* Integração com Excel, Pandas, Polars e Apache Arrow.
* Execução de SQL ANSI.
* Excelente desempenho para consultas agregadas.
* Suporte a funções analíticas (Window Functions).
* Instalação simples.



# Instalando

Python

```bash
pip install duckdb
```

CLI

```bash
duckdb
```

Abrindo um banco

```sql
.open analytics.duckdb
```



# Criando tabelas

```sql
CREATE TABLE vendas (

id INTEGER,

cliente VARCHAR,

produto VARCHAR,

categoria VARCHAR,

cidade VARCHAR,

valor DECIMAL(10,2),

data_venda DATE

);
```

Inserindo registros

```sql
INSERT INTO vendas VALUES

(1,'João','Notebook','Informática','São Carlos',5200,'2026-01-10'),

(2,'Maria','Mouse','Periféricos','Campinas',120,'2026-01-11'),

(3,'Pedro','Notebook','Informática','São Paulo',5100,'2026-01-13');
```

Visualizando dados

```sql
SELECT *

FROM vendas;
```



# Importando arquivos

CSV

```sql
SELECT *

FROM read_csv('vendas.csv');
```

Parquet

```sql
SELECT *

FROM read_parquet('vendas.parquet');
```

Todos os arquivos da pasta

```sql
SELECT *

FROM read_parquet('dados/*.parquet');
```

JSON

```sql
SELECT *

FROM read_json('pedidos.json');
```



# Filtrando dados

```sql
SELECT *

FROM vendas

WHERE valor > 1000;
```

Múltiplas condições

```sql
SELECT *

FROM vendas

WHERE cidade='São Carlos'

AND categoria='Informática';
```



# Ordenação

```sql
SELECT *

FROM vendas

ORDER BY valor DESC;
```



# LIMIT

```sql
SELECT *

FROM vendas

LIMIT 10;
```



# DISTINCT

```sql
SELECT DISTINCT cidade

FROM vendas;
```



# GROUP BY

```sql
SELECT

cidade,

SUM(valor)

FROM vendas

GROUP BY cidade;
```



# HAVING

```sql
SELECT

cidade,

SUM(valor)

FROM vendas

GROUP BY cidade

HAVING SUM(valor)>10000;
```



# CASE

```sql
SELECT

cliente,

CASE

WHEN valor>5000 THEN 'Premium'

ELSE 'Padrão'

END categoria_cliente

FROM vendas;
```



# JOIN

```sql
SELECT

v.cliente,

c.estado

FROM vendas v

JOIN clientes c

ON c.id=v.cliente_id;
```



# LEFT JOIN

```sql
SELECT *

FROM clientes c

LEFT JOIN vendas v

ON c.id=v.cliente_id;
```



# UNION

```sql
SELECT *

FROM vendas2025

UNION ALL

SELECT *

FROM vendas2026;
```



# Funções de agregação

```sql
COUNT(*)

SUM(valor)

AVG(valor)

MIN(valor)

MAX(valor)

MEDIAN(valor)

STDDEV(valor)
```



# Window Functions

Ranking

```sql
SELECT

cliente,

valor,

RANK() OVER(ORDER BY valor DESC)

FROM vendas;
```

Running Total

```sql
SELECT

data_venda,

SUM(valor)

OVER(

ORDER BY data_venda

)

FROM vendas;
```

Média móvel

```sql
SELECT

data_venda,

AVG(valor)

OVER(

ORDER BY data_venda

ROWS BETWEEN 2 PRECEDING

AND CURRENT ROW

)

FROM vendas;
```



# Trabalhando com datas

Ano

```sql
SELECT YEAR(data_venda)

FROM vendas;
```

Mês

```sql
SELECT MONTH(data_venda)

FROM vendas;
```

Dia

```sql
SELECT DAY(data_venda)

FROM vendas;
```

Agrupando por mês

```sql
SELECT

MONTH(data_venda),

SUM(valor)

FROM vendas

GROUP BY MONTH(data_venda);
```



# Strings

Maiúsculas

```sql
UPPER(cliente)
```

Minúsculas

```sql
LOWER(cliente)
```

Concatenação

```sql
CONCAT(nome,' ',sobrenome)
```

Substring

```sql
SUBSTRING(nome,1,5)
```



# Trabalhando com NULL

```sql
COALESCE(desconto,0)
```

```sql
IFNULL(desconto,0)
```



# CTE

```sql
WITH faturamento AS (

SELECT

cidade,

SUM(valor) total

FROM vendas

GROUP BY cidade

)

SELECT *

FROM faturamento

ORDER BY total DESC;
```



# Views

```sql
CREATE VIEW vendas_sp AS

SELECT *

FROM vendas

WHERE cidade='São Paulo';
```



# Exportando resultados

CSV

```sql
COPY (

SELECT *

FROM vendas

)

TO 'resultado.csv'

(FORMAT CSV, HEADER);
```

Parquet

```sql
COPY vendas

TO 'vendas.parquet'

(FORMAT PARQUET);
```



# EXPLAIN

```sql
EXPLAIN

SELECT *

FROM vendas

WHERE valor>1000;
```

Excelente para entender como o DuckDB executa cada consulta.



# PIVOT

```sql
PIVOT vendas

ON categoria

USING SUM(valor);
```

Ideal para criar tabelas dinâmicas usando SQL.



# UNPIVOT

```sql
UNPIVOT vendas

ON janeiro,

fevereiro,

março

INTO

NAME mes

VALUE faturamento;
```



# Funções estatísticas

```sql
CORR()

COVAR_POP()

MEDIAN()

MODE()

QUANTILE()

PERCENTILE_CONT()
```

Muito úteis em Ciência de Dados.



# Trabalhando com múltiplos arquivos

```sql
SELECT *

FROM read_parquet(

'datalake/**/*.parquet'

);
```

O DuckDB consulta centenas de arquivos simultaneamente.



# Integrando com Python

```python
import duckdb

df = duckdb.sql("""

SELECT

categoria,

SUM(valor)

FROM read_parquet('dados/*.parquet')

GROUP BY categoria

""").df()

print(df)
```

O resultado já retorna como um DataFrame do Pandas.



# Casos de uso reais

O DuckDB é uma excelente escolha para:

* Exploração de grandes conjuntos de dados.
* Processamento de arquivos Parquet em Data Lakes.
* Construção de notebooks analíticos.
* Preparação de dados para Machine Learning.
* Validação de pipelines de Engenharia de Dados.
* Criação de datasets para dashboards.
* Análise de logs em JSON.
* Consolidação de planilhas Excel.
* Integração com Polars, Pandas e Apache Arrow.
* Desenvolvimento local antes da execução em ambientes distribuídos.



# Dicas de desempenho

* Prefira arquivos Parquet para grandes volumes de dados.
* Selecione apenas as colunas necessárias em vez de usar `SELECT *`.
* Utilize filtros (`WHERE`) o mais cedo possível.
* Aproveite o particionamento de diretórios para reduzir leituras.
* Use `EXPLAIN` para entender planos de execução.
* Prefira funções analíticas (`OVER`) em vez de múltiplas subconsultas quando apropriado.



# Conclusão

O DuckDB não é apenas mais um banco de dados: ele representa uma mudança na forma de trabalhar com análise de dados. Sua combinação de simplicidade, desempenho e integração com formatos modernos como Parquet, JSON e Apache Arrow permite que analistas e engenheiros concentrem seus esforços na geração de valor, e não na configuração de infraestrutura.

Dominar seus comandos fundamentais — desde consultas básicas até funções analíticas, PIVOT, CTEs, exportação de resultados e integração com Python — torna o DuckDB uma ferramenta extremamente versátil para projetos de Ciência de Dados, Engenharia de Dados e Business Intelligence.

Se você trabalha diariamente com dados, vale a pena incorporar o DuckDB ao seu conjunto de ferramentas. Em muitos cenários, ele pode reduzir significativamente o tempo entre a pergunta de negócio e a resposta baseada em evidências.
