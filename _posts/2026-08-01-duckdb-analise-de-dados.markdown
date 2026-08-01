--- 
layout: post
title: "DuckDB na Prática: Como Analisar Dados em CSV, Excel, JSON e Parquet com SQL em Minutos"
date: 2026-08-01 09:00:00 -0300
categories: análise data analytics descritiva diagnóstica preditiva prescritiva cognitiva tempo real ciência dados business intelligence duckdb
---

![DuckDB]({{ site.url }}/assets/duckdb.png){:style="width: 100%" }

No [artigo anterior]({% link _posts/2026-08-01-os-6-tipos-de-analise-de-dados.markdown %}) vimos que existem diferentes tipos de análise de dados e que cada uma responde a perguntas específicas sobre um negócio.

Mas existe outra pergunta igualmente importante:

**Qual ferramenta utilizar para realizar essas análises?**

Durante muitos anos a resposta quase sempre foi a mesma:

* importar tudo para um banco de dados;
* criar tabelas;
* configurar servidores;
* realizar o ETL;
* somente então começar as análises.

Hoje existe uma alternativa extremamente poderosa.

Seu nome é **DuckDB**.

Ele permite consultar arquivos CSV, Excel, JSON e Parquet diretamente com SQL, dispensando grande parte da infraestrutura tradicional para análises exploratórias.

Neste artigo vamos conhecer o DuckDB e descobrir por que ele vem conquistando analistas de dados, cientistas de dados e engenheiros de dados.



# O que é o DuckDB?

O DuckDB é um banco de dados analítico (OLAP) extremamente leve, rápido e embarcado (*embedded*).

Ele funciona de maneira semelhante ao SQLite, porém foi desenvolvido especificamente para cargas analíticas.

Isso significa que ele foi otimizado para executar consultas envolvendo milhões de registros utilizando pouca memória.

Sua principal característica é simples:

**Levar o processamento até os dados.**

Em muitos casos você nem precisa importar os arquivos.

Pode consultá-los diretamente.



# Onde o DuckDB realmente brilha?

DuckDB foi criado para análise de dados.

Ele não substitui PostgreSQL, MySQL ou SQL Server em aplicações transacionais.

Cada ferramenta possui seu propósito.

DuckDB destaca-se principalmente em:

* Análise exploratória de dados (EDA)
* Ciência de Dados
* Engenharia de Dados
* Business Intelligence
* Processamento de arquivos Parquet
* Integração com Python
* Integração com Jupyter Notebook
* Integração com Pandas e Polars
* Processamento local de grandes volumes

Imagine possuir uma pasta contendo centenas de arquivos Parquet.

Com DuckDB basta executar uma consulta SQL.

Não é necessário importar nada.



# Instalação

## Python

```bash
pip install duckdb
```

Ou utilizando apenas o terminal:

```bash
duckdb
```

Também existe suporte para R, Java, Node.js e diversas outras linguagens.



# Exemplo 1 — Analisando um CSV

Imagine o arquivo:

```text
vendas.csv
```

```csv
cliente,produto,valor,cidade
João,Notebook,5200,São Carlos
Maria,Mouse,120,Ribeirão Preto
Pedro,Notebook,5100,São Paulo
Ana,Monitor,1600,São Carlos
```

Consultar esse arquivo é muito simples:

```sql
SELECT *
FROM read_csv('vendas.csv');
```

Agora vamos descobrir o faturamento por cidade.

```sql
SELECT
    cidade,
    SUM(valor) AS faturamento
FROM read_csv('vendas.csv')
GROUP BY cidade
ORDER BY faturamento DESC;
```

Perceba que nunca criamos uma tabela.

O arquivo foi consultado diretamente.



# Exemplo 2 — Trabalhando com Excel

Imagine um arquivo chamado:

```text
clientes.xlsx
```

Após instalar a extensão correspondente, podemos consultar o conteúdo usando SQL.

```sql
SELECT *
FROM 'clientes.xlsx';
```

Agora podemos descobrir quantos clientes existem por estado.

```sql
SELECT
    estado,
    COUNT(*)
FROM 'clientes.xlsx'
GROUP BY estado;
```

Para muitos analistas isso elimina a necessidade de importar planilhas para outro banco antes da análise.



# Exemplo 3 — Consultando JSON

Suponha o arquivo:

```json
{
 "cliente":"João",
 "cidade":"São Carlos",
 "valor":5200
}
```

Consultar JSON também é simples.

```sql
SELECT *
FROM read_json('pedidos.json');
```

Agrupando por cidade:

```sql
SELECT
cidade,
SUM(valor)
FROM read_json('pedidos.json')
GROUP BY cidade;
```

Isso é extremamente útil para analisar logs, APIs e eventos exportados em JSON.



# Exemplo 4 — O poder do Parquet

Parquet é um formato colunar muito utilizado em Data Lakes.

É justamente aqui que DuckDB mais impressiona.

Imagine uma pasta contendo:

```text
dados/

vendas_2024.parquet

vendas_2025.parquet

vendas_2026.parquet
```

Consultar todos eles:

```sql
SELECT *
FROM read_parquet('dados/*.parquet');
```

Somar o faturamento:

```sql
SELECT
SUM(valor)
FROM read_parquet('dados/*.parquet');
```

Agrupar por categoria:

```sql
SELECT
categoria,
SUM(valor)
FROM read_parquet('dados/*.parquet')
GROUP BY categoria;
```

DuckDB consegue ler apenas as colunas necessárias, reduzindo drasticamente o volume de dados processado.

Essa otimização é um dos principais motivos de seu excelente desempenho.



# Juntando diferentes formatos em uma única análise

Uma das funcionalidades mais interessantes do DuckDB é combinar fontes distintas em uma única consulta.

Imagine:

* clientes.xlsx
* vendas.parquet
* metas.csv

Podemos fazer um JOIN entre essas informações utilizando SQL.

```sql
SELECT

c.nome,

SUM(v.valor),

m.meta

FROM read_parquet('vendas.parquet') v

JOIN 'clientes.xlsx' c

ON c.id = v.cliente_id

JOIN read_csv('metas.csv') m

ON c.estado = m.estado

GROUP BY c.nome,m.meta;
```

Na prática, isso reduz significativamente o tempo gasto preparando dados antes da análise.



# Quando usar DuckDB?

DuckDB é excelente para:

* análises exploratórias;
* dashboards locais;
* notebooks em Python;
* processamento de arquivos Parquet;
* integração com Pandas e Polars;
* validação de dados;
* prototipação rápida de consultas;
* processamento de datasets de milhões de linhas em uma única máquina.



# Quando não utilizar?

DuckDB não foi desenvolvido para substituir bancos transacionais.

Para aplicações web, ERPs ou sistemas que exigem milhares de escritas concorrentes, bancos como PostgreSQL continuam sendo a melhor escolha.

A estratégia mais comum é combinar as duas tecnologias:

* PostgreSQL para armazenar os dados da aplicação;
* DuckDB para realizar análises rápidas sobre exportações ou arquivos do Data Lake.

Cada ferramenta faz aquilo para o qual foi projetada.



# Conclusão

O DuckDB representa uma nova forma de analisar dados. Em vez de gastar tempo importando arquivos para um banco de dados, ele permite consultar diretamente CSV, Excel, JSON e Parquet utilizando SQL, tornando o processo muito mais ágil.

Seu desempenho, aliado à simplicidade de uso e à integração com ferramentas como Python, Pandas e Polars, faz dele uma excelente escolha para análises exploratórias, pipelines de Engenharia de Dados e projetos de Ciência de Dados.

Se você ainda não experimentou o DuckDB, vale a pena dedicar alguns minutos para instalá-lo e testar seus próprios datasets. É muito provável que ele se torne uma das ferramentas mais úteis do seu dia a dia como analista ou engenheiro de dados.

Nos próximos artigos do Tudo Programado Blog, vamos aprofundar esse tema mostrando como integrar o DuckDB com Python, Pandas, Polars e Apache Iceberg, além de construir pipelines analíticos modernos utilizando apenas ferramentas open source.
