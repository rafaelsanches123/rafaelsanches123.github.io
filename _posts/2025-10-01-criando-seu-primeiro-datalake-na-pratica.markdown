--- 
layout: post
title:  "Criando seu primeiro Data Lake na prática com MinIO"
date:   2025-10-01 20:00:00 -0300
categories: datalake lake data dados bigdata DataLake MinIO
---

![Data-Lake]({{ site.url }}/assets/data-lake-minio.png){:style="width: 100%" }

# Criando um Data Lake na Prática com MinIO, Docker e Docker Compose

Nos últimos anos, o **Data Lake** tem se tornado uma das principais arquiteturas para armazenamento de dados em empresas de todos os portes. Ele permite armazenar dados **estruturados, semiestruturados e não estruturados** em um repositório centralizado, com baixo custo e alta escalabilidade.

Mas afinal, como podemos **colocar a mão na massa** e criar um Data Lake para estudos ou até para projetos internos?
Neste post, vamos montar um **Data Lake simples usando o MinIO, Docker e Docker Compose**.

## O que é um Data Lake?

Um [Data Lake]({% link _posts/2024-08-25-o-que-e-data-lake.markdown %}){:target="_blank"} é um repositório central que armazena dados em seu formato bruto, podendo ser texto, JSON, imagens, vídeos, logs, tabelas e muito mais. Ele difere de um Data Warehouse, que armazena dados já tratados e estruturados.

Características principais:

* **Flexibilidade**: aceita qualquer tipo de dado.
* **Escalabilidade**: cresce conforme a necessidade.
* **Baixo custo**: uso de armazenamento em nuvem ou soluções locais.
* **Integração**: base para projetos de Big Data, Analytics e Machine Learning.

## O que é o MinIO?

[MinIO](https://min.io/) é uma solução **compatível com o protocolo S3 da AWS**. Ele é leve, rápido e pode ser executado facilmente em containers, tornando-se uma excelente alternativa para montar um **Data Lake local** para testes ou até ambientes de produção em menor escala.

## Preparando nosso ambiente

Você precisa ter instalado no seu computador:

* [Docker]({% link _posts/2023-07-16-instalando-e-configurando-o-docker.markdown %}){:target="_blank"}
* [Docker Compose]({% link _posts/2024-12-18-instalando-docker-compose.markdown %}){:target="_blank"}

Para verificar se está tudo certo vá no seu terminal e execute os comandos:

```bash
docker -v
docker compose version
```

## Criando o Docker Compose para o MinIO

Crie um arquivo chamado `docker-compose.yml` com o seguinte conteúdo:

```yaml
version: '3.8'

services:
  minio:
    image: minio/minio:RELEASE.2025-02-03T21-03-04Z-cpuv1
    container_name: minio
    ports:
      - "9000:9000"
      - "9001:9001"
    environment:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
    volumes:
      - ./data:/data
    command: server /data --console-address ":9001"
```

👉 Explicando:

* `MINIO_ROOT_USER` e `MINIO_ROOT_PASSWORD`: credenciais de acesso.
* `volumes`: mapeia os dados para o host local.
* `9000`: porta da API S3.
* `9001`: console web para gerenciar buckets e arquivos.
* A versão RELEASE.2025-02-03T21-03-04Z-cpuv1 da imagem docker do minio é necessária para ter acesso aos mesmos recursos apresentados no decorrer desse post. Não use a versão mais recente/atual se não você não terá mais acesso ao recuros disponíveis nessa versão utilizada nessa aplicação prática de data lake.

## Colocando a infraestrutura do seu Data Lake para funcionar

No terminal, execute:

```bash
docker compose up -d
```

Agora acesse o console do MinIO em:
👉 [http://localhost:9001](http://localhost:9001)

Use o usuário e senha definidos no `docker-compose.yml` (`minioadmin / minioadmin`).

## Criando um Bucket e Subindo Arquivos

No console do MinIO, crie um **bucket** chamado `entrada` e faça upload de alguns arquivos (CSV, JSON, imagens, etc.).

Uma visão prática do uso do MinIO:

Use seu login e senha para acessar o painel gerencial do MinIO: 

**Username**: minioadmin

**Password**: minioadmin

![DataLake-Home]({{ site.url }}/assets/login.png){:style="width: 100%" }

Na tela principal você tem acesso a todos os recursos que o MinIO oferece a você para gerenciar seus dados. É possível observar que você tem opções direcionadas aos usuários do ambiente e aos administradores.

Clique na opção **Create a Bucket** para criar o seu primeiro e começarmos a brincar. 

![DataLake-Home]({{ site.url }}/assets/home.png){:style="width: 100%" }

Nessa tela você informa qual nome seu bucket vai se chamar dentro do seu repositório centralizado de dados. No exemplo da imagem eu chamei de entrada, mas poderia ser qualquer outra coisa.

![DataLake-Home]({{ site.url }}/assets/criar-bucket.png){:style="width: 100%" }

Após criar o bucket você vai ter essa visão de usuário. Aqui você pode acessar o seu bucket clicando sobre ele ou criar um novo bucket na opção 'Create Bucket +'. Nesse momento vamos apenas clicar no **bucket entrada** para explorar mais nosso datalake.

![DataLake-Home]({{ site.url }}/assets/bucket-criado.png){:style="width: 100%" }

Aqui vemos o nosso bucket criado e nessa tela que vamos começar colocar dados dentro do nosso bucket.

![DataLake-Home]({{ site.url }}/assets/tela-gestao-bucket.png){:style="width: 100%" }

Nessa tela você tem a opção de fazer upload de seus arquivos para dentro do bucket entrada. Para testar ele funcionado eu crie na minha maquina local dentro da minha pasta Downloads 4 arquivos teste.csv, teste.json, teste.parquet e teste.xml para testar o envio de dados para o nosso bucket.

![DataLake-Home]({{ site.url }}/assets/upload-arquivos-bucket.png){:style="width: 100%" }

**A seguir vou mostrar algumas opções para você brincar ainda mais com seu datalake.**

Vamos começar falando sobre **Chaves de Acesso**:

A função **Access Keys** do **MinIO** permite criar **credenciais de acesso (Access Key e Secret Key)** que funcionam de forma semelhante a um **usuário e senha** para acessar o servidor MinIO via **API, SDK ou ferramentas como `mc`, `aws cli` ou `curl`**.

Em resumo, ela permite que você:

1. 🔐 **Autentique-se** no MinIO sem precisar usar a conta root.
2. 📦 **Controle acessos** a buckets e objetos por meio de políticas associadas (como `readwrite`, `readonly`, etc.).
3. 👥 **Crie chaves temporárias ou específicas** para aplicações, serviços ou usuários diferentes.
4. 🔄 **Revogue ou substitua credenciais** facilmente sem afetar outros acessos.

💡 **Em outras palavras:**
As *access keys* são o mecanismo de autenticação e autorização do MinIO, permitindo controlar **quem pode acessar o quê** dentro do seu ambiente de armazenamento.

![DataLake-Home]({{ site.url }}/assets/access-keys-minio.png){:style="width: 100%" }

Vamos aprender agora sobre **Policies**:

A função **Policies** do **MinIO** permite **definir e gerenciar regras de permissão** que controlam **o que um usuário, grupo ou aplicação pode fazer** dentro do ambiente.

Em resumo, ela permite que você:

1. 🧾 **Crie políticas de acesso** (em formato JSON) especificando **ações permitidas** — como listar, ler, gravar ou deletar objetos.
2. 🔗 **Associe essas políticas** a usuários, grupos ou *access keys*.
3. 🚫 **Restrinja acessos** a determinados buckets, pastas ou objetos.
4. 🧰 **Implemente controle de acesso fino (RBAC)** dentro do MinIO.

💡 **Em outras palavras:**
As *policies* são o **conjunto de regras que dizem “quem pode fazer o quê”** no MinIO. Elas funcionam como as políticas do IAM (Identity and Access Management) da AWS S3.

![DataLake-Home]({{ site.url }}/assets/bucket-policies.png){:style="width: 100%" }

Vamos aprender agora sobre **Groups**:

A função **Groups** do **MinIO** permite **organizar usuários em grupos** para **gerenciar permissões de forma centralizada e eficiente**.

Em resumo, ela permite que você:

1. 👥 **Agrupe vários usuários** que precisam das mesmas permissões.
2. 🔗 **Atribua uma ou mais políticas** (*policies*) a todo o grupo — em vez de configurar usuário por usuário.
3. ⚙️ **Simplifique a administração de acessos**, aplicando mudanças de permissão a todos os membros de uma só vez.
4. 🚪 **Controle quem entra ou sai** do grupo, mantendo a segurança e consistência.

💡 **Em outras palavras:**
Os *groups* são uma forma de **gerenciar permissões coletivamente**, facilitando o controle de acesso em ambientes com muitos usuários.

![DataLake-Home]({{ site.url }}/assets/minio-groups.png){:style="width: 100%" }


Caso você já seja um **usuário avançado** você pode fazer tudo o que mencionamos anteriormente com o **MinIO Client (mc)** via terminal (Opcional):

```bash
# Baixar o cliente
wget https://dl.min.io/client/mc/release/linux-amd64/mc
chmod +x mc
sudo mv mc /usr/local/bin/

# Configurar conexão com o MinIO
mc alias set local http://localhost:9000 minioadmin minioadmin

# Apenas um exemplo ilustrativo. Aqui nosso bucket chama-se data-lake.
# Criar bucket
mc mb local/data-lake

# Apenas um exemplo ilustrativo
# Enviar arquivos
mc cp ./meus_dados.csv local/data-lake/
```

## E agora?

Pronto! 🎉 Você acabou de criar um **Data Lake local** usando MinIO e Docker.
Esse ambiente pode servir de base para integrar com ferramentas de **Spark, Hive, Airflow, dbt, ou até pipelines de Machine Learning**.

Nos próximos posts, podemos evoluir esse setup para:

* Processar dados com **Apache Spark**.
* Validar dados com **Soda Core**.
* Criar pipelines de ingestão com **Airbyte ou Kafka**.
* Construir Arquiteturas de Dados **Data LakeHouse**.
* Construir Arquiteturas de Dados **Data Mesh**.

## ✅ Conclusão

O **MinIO** é uma ferramenta poderosa para simular e até construir Data Lakes em ambientes corporativos. Usando **Docker e Docker Compose**, conseguimos montar rapidamente um ambiente de estudo prático que pode ser expandido para projetos reais.