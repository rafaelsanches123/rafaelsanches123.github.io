---
layout: post
title:  "Garantindo Qualidade de Dados com Great Expectations: Guia Prático com arquivo CSV"
date:   2025-07-22 08:00:00 -0300
categories: Qualidade Dados DataQuality Governança Arquitetura
---

![QualidadeDeDadosNaPratica]({{ site.url }}/assets/qualidade-de-dados-com-great-expectations.png){:style="width: 100%" }

A qualidade de dados é um dos pilares de uma arquitetura de dados robusta. Dados incorretos, incompletos ou inconsistentes podem comprometer análises, modelos preditivos e decisões estratégicas. Uma das ferramentas open source mais poderosas para garantir a qualidade dos dados é o **Great Expectations**.

Neste post, vou explicar o que é essa ferramenta, por que ela é tão importante e como você pode começar a utilizá-la de forma simples com arquivos **CSV**.

## O que é o Great Expectations?

O **Great Expectations (GE)** é uma biblioteca open source para validação, documentação e perfilamento de dados. Ele permite que você defina **expectativas** (regras) sobre os dados que você espera encontrar em seus pipelines, garantindo que eles atendam a padrões de qualidade antes de serem consumidos.

Algumas funcionalidades principais:

* Validação de dados com regras customizáveis.
* Geração automática de documentação em HTML.
* Integração com diversas fontes de dados: arquivos, bancos relacionais, Spark, Pandas, Snowflake e outros.
* Compatibilidade com CI/CD e DataOps.

## Quando usar o Great Expectations?

* Ao validar dados antes de carregar no Data Warehouse.
* Ao monitorar a qualidade de dados em pipelines ELT/ETL.
* Em times de dados que querem aplicar princípios de *Data Contracts* ou *Data as a Product*.
* Em auditorias de dados ou conformidade regulatória.

## Mãos na Massa: Usando o GE com um Arquivo CSV

### 🎯 Objetivo:

Validar um arquivo CSV contendo dados de vendas, aplicando regras como:

* A coluna `valor_total` deve ser maior que 0.
* A coluna `categoria` deve conter apenas valores esperados.
* A coluna `data_venda` deve conter datas válidas.

### 🛠️ Pré-requisitos

* Python 3.8+
* Ambiente virtual configurado (opcional, mas recomendado)

### 1. Instale o Great Expectations

```bash
pip install great-expectations
```

### 2. Inicialize um projeto

```bash
great_expectations init
```

Isso criará a estrutura de pastas `great_expectations/`.

### 3. Prepare um CSV de exemplo

Crie um arquivo chamado `vendas.csv`:

```csv
id_venda,produto,categoria,data_venda,valor_total
1,Notebook,Eletrônicos,2023-06-01,3500.00
2,Mouse,Eletrônicos,2023-06-02,50.00
3,Cadeira,Escritório,2023-06-03,0.00
4,Caneta,Papelaria,2023-06-04,5.00
5,Celular,Eletrônicos,2023-06-05,1500.00
```

Salve-o na raiz do seu projeto.

### 4. Crie um datasource baseado no CSV

Execute:

```bash
great_expectations datasource new
```

Siga o assistente interativo:

* Nome: `vendas_datasource`
* Tipo: `Pandas`
* Caminho: `./vendas.csv`

Ele criará um datasource do tipo `Pandas` apontando para o CSV.

#### 💡 Resumo simples dessa etapa:

Você está dizendo para o **Great Expectations (GE)**:

> “Olha, eu quero que você leia os dados deste **arquivo CSV** aqui, porque é nele que quero aplicar minhas regras de qualidade.”

### 5. Crie um *Expectation Suite*

```bash
great_expectations suite new
```

* Nome: `vendas_suite`
* Escolha "interactive editor"

Ao final, o navegador será aberto.

#### 💡 Resumo simples dessa etapa:

Você está dizendo para o Great Expectations:

> “Agora que você sabe onde estão os dados, eu quero criar um **conjunto de regras** que os dados precisam seguir.”

Esse conjunto de regras recebe o nome técnico de **Expectation Suite** — traduzindo: um *conjunto de expectativas*.

### 6. Crie as regras (expectativas)

Dentro do notebook interativo aberto, adicione regras como:

```python
# Carrega dados
batch = context.get_batch(
    BatchRequest(
        datasource_name="vendas_datasource",
        data_connector_name="default_inferred_data_connector_name",
        data_asset_name="vendas.csv",
        runtime_parameters={"path": "./vendas.csv"},
        batch_identifiers={"default_identifier_name": "default"},
    )
)

# Cria validador
validator = context.get_validator(
    batch_request=batch,
    expectation_suite_name="vendas_suite"
)

# Regras
validator.expect_column_values_to_be_in_set("categoria", ["Eletrônicos", "Escritório", "Papelaria"])
validator.expect_column_values_to_be_between("valor_total", min_value=0.01)
validator.expect_column_values_to_match_strftime_format("data_venda", "%Y-%m-%d")

validator.save_expectation_suite(discard_failed_expectations=False)
```

Salve e feche o notebook.

#### 💡 Resumo simples dessa etapa:

Agora que o Great Expectations já:

* sabe **onde estão os dados** (datasource),
* tem uma **caixinha onde vai guardar as regras** (expectation suite),

... chegou a hora de **escrever as regras de verdade** que os dados precisam seguir.

Essas regras são chamadas de **expectativas** (*expectations*, em inglês).

### 7. Execute a validação

Agora você pode validar o arquivo:

```bash
great_expectations checkpoint new vendas_checkpoint
```

Configure o checkpoint para usar:

* Expectation Suite: `vendas_suite`
* Data Asset: `vendas.csv`

Depois, execute:

```bash
great_expectations checkpoint run vendas_checkpoint
```

#### 💡 Resumo simples dessa etapa:

Agora que:

1. Você **definiu onde estão os dados**,
2. Criou um **conjunto de regras (expectation suite)**,
3. E escreveu **regras específicas** para os dados,

... chegou a hora de **colocar tudo para rodar**. Ou seja, **testar se os dados estão realmente seguindo as regras** que você criou.

### 8. Verifique os resultados

Após a execução, o GE gera um relatório HTML no diretório:

```
great_expectations/uncommitted/data_docs/local_site/index.html
```

Abra o arquivo no navegador e veja o resultado da validação.

#### 💡 Resumo simples dessa etapa:

Você **já executou a validação** dos seus dados com o Great Expectations (GE). Agora, é hora de **ver o que aconteceu**.
Ou seja:

> “Os dados passaram no teste? Ou tem alguma coisa errada?”

#### 🧪 No mundo dos dados, o que o GE mostra?

Após rodar a validação, o Great Expectations gera **relatórios automáticos** que te mostram:

* Quais regras **foram atendidas**,
* Quais **falharam**,
* Em qual **coluna** do seu arquivo isso ocorreu,
* E **quantas linhas** apresentaram problema.


## Conclusão

O **Great Expectations** é uma ferramenta poderosa para automatizar validações de qualidade de dados. Neste post, mostramos como dar os primeiros passos com arquivos CSV, criando uma suite de validação e executando checkpoints.

No próximo passo, você pode:

* Automatizar via cron ou Airflow.
* Integrar com fontes como PostgreSQL, S3, Spark ou Data Lakes.
* Versão das expectativas com controle de código-fonte.

## Recursos úteis

* [Site oficial](https://greatexpectations.io/)
* [Documentação](https://docs.greatexpectations.io/)
* [Repositório no GitHub](https://github.com/great-expectations/great_expectations)

Se você gostou desse conteúdo, compartilhe e continue acompanhando o blog! 🚀