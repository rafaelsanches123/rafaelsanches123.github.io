---
layout: post
title:  "Apache Airflow"
date:   2024-09-30 00:00:00 -0300
categories: data data-engineering data-pipeline pipeline apache airflow apache-airflow
---

![Tubulação de Canos]({{ site.url }}/assets/airflow-tubulacao.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post vou apresentar para vocês uma ferramenta incrível que você não pode deixar de conhecer se você trabalho com dados. Se você está migrando para a área de dados, se já é um profissional da área de dados ou se simplesmente gosta de aprender algo novo.

Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

# O que é o Apache Airflow?

O **Apache Airflow** é uma plataforma open-source usada para **orquestrar, agendar e monitorar workflows** (fluxos de trabalho). Ele é amplamente utilizado para automatizar pipelines de dados, garantindo que tarefas relacionadas à coleta, transformação, limpeza e análise de dados sejam realizadas de maneira eficiente e em ordem correta. Foi desenvolvido inicialmente pelo Airbnb em 2014 e depois se tornou parte da **Apache Software Foundation**, ganhando muita popularidade no mundo da engenharia de dados.

No Airflow, os workflows são definidos como **DAGs** (Directed Acyclic Graphs, ou Grafo Acíclico Direcionado), que determinam a sequência e as dependências entre as tarefas.

### Componentes principais do Apache Airflow

1. **DAG (Directed Acyclic Graph)**:  
   Uma DAG é a representação visual do fluxo de trabalho. Ela contém as tarefas e a ordem em que elas devem ser executadas, respeitando as dependências.

2. **Tarefa (Task)**:  
   Cada nó de uma DAG é uma tarefa individual, que pode realizar diversas operações, como execução de scripts Python, movimentação de dados, chamadas de APIs, entre outras. O Airflow executa essas tarefas de acordo com a ordem e dependências definidas na DAG.

3. **Scheduler**:  
   O componente que determina quando as tarefas de uma DAG devem ser executadas, de acordo com os horários e intervalos configurados.

4. **Executor**:  
   O executor define como as tarefas serão realmente executadas. Pode ser em modo sequencial, local (usando múltiplos processos no mesmo servidor) ou distribuído (em múltiplas máquinas).

5. **Webserver**:  
   O webserver oferece uma interface gráfica onde os usuários podem monitorar e gerenciar os workflows, visualizar logs, acionar DAGs manualmente e verificar o status das execuções.

6. **Metadatabase**:  
   Um banco de dados que armazena o estado das DAGs, tarefas e logs, além de informações sobre a execução das DAGs.

### Usos do Apache Airflow no Mundo dos Dados

O Airflow é amplamente utilizado no campo da engenharia de dados e ciência de dados, principalmente para **automação de pipelines de dados complexos**. Seus principais usos incluem:

1. **ETL (Extração, Transformação e Carga de Dados)**:  
   Uma das aplicações mais comuns do Airflow é em pipelines de ETL, onde ele coordena a extração de dados de diversas fontes, realiza transformações e carrega os dados em um banco de dados ou data warehouse. Ele ajuda a agendar e automatizar essas operações de maneira eficiente.

2. **Orquestração de Pipelines de Dados**:  
   O Airflow é ideal para organizar pipelines de dados que envolvem várias etapas dependentes entre si. Por exemplo, você pode ter um processo que envolve coleta de dados de uma API, armazenamento no banco de dados, limpeza de dados, e depois um modelo de machine learning que será treinado sobre esses dados — tudo isso pode ser orquestrado com o Airflow.

3. **Automação de Workflows de Machine Learning**:  
   Para fluxos de trabalho de Machine Learning, o Airflow pode orquestrar a coleta de dados, a preparação, o treinamento de modelos e até mesmo o agendamento de previsões automáticas. Ele é usado em pipelines de MLOps para treinar modelos em horários específicos ou após a chegada de novos dados.

4. **Integração com Ferramentas de Big Data**:  
   O Airflow pode integrar com ferramentas como **Hadoop**, **Spark**, **Presto** e outras soluções de big data para orquestrar o processamento de dados em larga escala. Ele também pode disparar jobs nesses sistemas e monitorar suas execuções.

5. **Pipeline de Dados em Ambientes de Nuvem**:  
   Ele pode ser usado em conjunto com serviços na nuvem, como **AWS** (S3, Redshift, EMR), **GCP** (BigQuery, Cloud Storage) e **Azure**, para orquestrar pipelines de dados distribuídos entre várias ferramentas e serviços.

6. **Monitoramento e Notificação de Falhas**:  
   O Airflow permite que você configure notificações de sucesso ou falha, de forma que a equipe de engenharia de dados seja alertada sempre que algo der errado no pipeline. Ele também permite reiniciar automaticamente tarefas que falharam, garantindo maior robustez e confiabilidade.

### Vantagens do Apache Airflow

- **Extensível**: Pode ser customizado com novos operadores, sensores e hooks para atender a qualquer necessidade de workflow.
- **Escalável**: Pode ser usado em pequenas máquinas ou em grandes clusters distribuídos.
- **Interface Intuitiva**: A interface web facilita o monitoramento e a gestão dos pipelines de dados.
- **Automação e Programação**: Facilita o agendamento de pipelines complexos com regras de dependência entre tarefas.
- **Integrações**: Suporte nativo a uma ampla gama de tecnologias, como bancos de dados, APIs, ferramentas de big data, etc.

### Desafios e Considerações

Embora seja uma ferramenta poderosa, o Airflow tem alguns desafios:
- **Curva de Aprendizado**: Para definir pipelines, você escreve código Python, o que pode ser intimidador para quem não tem familiaridade com programação.
- **Sobrecarga de Infraestrutura**: Para grandes volumes de dados e pipelines altamente distribuídos, a configuração e manutenção do Airflow podem exigir uma infraestrutura mais complexa.
- **Escalabilidade em Execuções Massivas**: Em casos de pipelines massivos, pode ser necessário otimizar o sistema para garantir um bom desempenho, usando, por exemplo, o **Celery Executor** ou o **Kubernetes Executor** para escalabilidade horizontal.

### Conclusão

O Apache Airflow é uma ferramenta essencial no mundo da engenharia de dados, permitindo a orquestração de workflows complexos, o que facilita a automação e a confiabilidade em pipelines de dados. Ele é amplamente utilizado em empresas que lidam com grandes volumes de dados ou têm processos de dados distribuídos e complexos.

A seguir, vou mostrar um passo a passo para configurar o Airflow com Docker Compose.

# Passos para configurar o Airflow com Docker Compose:

1. **Instale o Docker e Docker Compose**  
   Se ainda não tiver o Docker e o Docker Compose instalados, você pode seguir as instruções no site oficial:
   - [Docker](https://docs.docker.com/get-docker/)
   - [Docker Compose](https://docs.docker.com/compose/install/)

2. **Crie o arquivo `docker-compose.yaml`**

   Em uma pasta dedicada para o Airflow, crie um arquivo chamado `docker-compose.yaml` com o seguinte conteúdo básico:

   ```yaml
   version: '3'
   services:
     postgres:
       image: postgres:13
       environment:
         POSTGRES_USER: airflow
         POSTGRES_PASSWORD: airflow
         POSTGRES_DB: airflow
       volumes:
         - ./dags:/opt/airflow/dags
         - ./logs:/opt/airflow/logs
         - ./plugins:/opt/airflow/plugins
       healthcheck:
         test: ["CMD-SHELL", "pg_isready -U airflow"]
         interval: 10s
         retries: 5

     webserver:
       image: apache/airflow:2.5.0
       depends_on:
         - postgres
       environment:
         AIRFLOW__CORE__LOAD_EXAMPLES: 'false'
         AIRFLOW__CORE__EXECUTOR: LocalExecutor
         AIRFLOW__DATABASE__SQL_ALCHEMY_CONN: postgresql+psycopg2://airflow:airflow@postgres:5432/airflow
       ports:
         - "8080:8080"
       volumes:
         - ./dags:/opt/airflow/dags
         - ./logs:/opt/airflow/logs
         - ./plugins:/opt/airflow/plugins
       command: webserver

     scheduler:
       image: apache/airflow:2.5.0
       depends_on:
         - webserver
       environment:
         AIRFLOW__CORE__EXECUTOR: LocalExecutor
         AIRFLOW__DATABASE__SQL_ALCHEMY_CONN: postgresql+psycopg2://airflow:airflow@postgres:5432/airflow
       volumes:
         - ./dags:/opt/airflow/dags
         - ./logs:/opt/airflow/logs
         - ./plugins:/opt/airflow/plugins
       command: scheduler
   ```

   Nesse arquivo, temos três serviços principais:
   - **Postgres**: o banco de dados para o Airflow.
   - **Webserver**: a interface web do Airflow.
   - **Scheduler**: o componente que agenda e executa as DAGs (Directed Acyclic Graphs).

3. **Configurar variáveis de ambiente**  
   Para que o Airflow funcione corretamente, você pode configurar variáveis de ambiente no arquivo `docker-compose.yaml`, como a conexão com o banco de dados, o executor, entre outros. A configuração acima já inclui algumas variáveis, como a conexão com o Postgres e a desativação do carregamento de exemplos.

4. **Inicialize o banco de dados do Airflow**

   Antes de rodar o Airflow, é necessário inicializar o banco de dados:

   ```bash
   docker-compose run --rm webserver airflow db init
   ```

   Isso criará todas as tabelas necessárias no banco de dados.

5. **Suba os serviços com o Docker Compose**

   Agora, você pode rodar todos os serviços com o seguinte comando:

   ```bash
   docker-compose up
   ```

6. **Acessar a interface web**

   Após subir os serviços, você pode acessar a interface web do Airflow no navegador, na porta `8080`. Abra o navegador e vá para:

   ```
   http://localhost:8080
   ```

   O usuário e senha padrão para o login na interface do Airflow são:
   - **Usuário**: `airflow`
   - **Senha**: `airflow`

7. **Gerenciar DAGs**

   Agora você pode adicionar DAGs na pasta `dags` do seu diretório, e elas aparecerão automaticamente na interface web.

### Conclusão

Com essa configuração, você terá o Airflow rodando localmente com o Docker Compose, o que facilita bastante o desenvolvimento e a execução de pipelines de dados. Caso precise de uma configuração mais avançada (por exemplo, utilizando o **CeleryExecutor** para executar tarefas em paralelo), é possível modificar o arquivo `docker-compose.yaml` conforme necessário.

# Dica para o caso de ocorrer algum erro de permissão

Durante os passos anteriores se obtiver o seguinte erro "PermissionError: [Errno 13] Permission denied: '/opt/airflow/logs/scheduler'":

O erro `PermissionError: [Errno 13] Permission denied` geralmente ocorre porque o contêiner do Docker não tem permissão para acessar ou criar pastas e arquivos no sistema de arquivos local, especificamente no diretório onde você mapeou os volumes para o Airflow.

A pasta `/opt/airflow/logs/scheduler` mencionada no erro está dentro do contêiner do Docker, mas ela está mapeada para um diretório local (no seu sistema), conforme definido no `docker-compose.yaml`:

```yaml
volumes:
  - ./logs:/opt/airflow/logs
```

### Solução para corrigir o erro:

1. **Garantir permissões corretas nas pastas locais**

   Primeiro, você precisa garantir que o usuário que está rodando o contêiner do Docker tenha permissões de leitura e gravação na pasta local onde os logs, DAGs e plugins são armazenados.

   Para fazer isso, vá até o diretório onde estão as pastas `dags`, `logs` e `plugins` no seu sistema local e execute os seguintes comandos para garantir as permissões corretas:

   ```bash
   sudo mkdir -p logs dags plugins
   sudo chmod -R 777 logs dags plugins
   ```

   O comando `chmod -R 777` concede permissões completas de leitura, gravação e execução para todos os usuários (temporariamente). Se estiver em um ambiente de produção ou mais seguro, você deve ajustar as permissões de acordo com as necessidades, concedendo-as apenas ao grupo ou usuário apropriado.

2. **Remover volumes antigos e reiniciar os serviços**

   Depois de ajustar as permissões, você pode garantir que os volumes anteriores criados pelo Docker sejam removidos, para evitar problemas de cache.

   Primeiro, derrube todos os serviços e remova os volumes com os seguintes comandos:

   ```bash
   docker-compose down --volumes --remove-orphans
   ```

   Agora, reinicie os serviços:

   ```bash
   docker-compose up
   ```

3. **Verificar o usuário do contêiner (opcional)**

   Caso o problema persista, pode ser necessário garantir que o contêiner do Airflow esteja sendo executado com o usuário correto, com permissões adequadas.

   Você pode verificar se o contêiner está sendo executado com um usuário não privilegiado e tentar rodá-lo como `root` (somente para fins de desenvolvimento) adicionando a seguinte linha no seu `docker-compose.yaml` na seção de cada serviço (`webserver`, `scheduler`, etc.):

   ```yaml
   user: "0:0"
   ```

   Isso força o contêiner a ser executado com o usuário `root` dentro do contêiner.

4. **Reiniciar a inicialização do banco de dados**

   Depois de corrigir o problema de permissão, você pode inicializar o banco de dados novamente (caso tenha sido corrompido ou a inicialização falhou anteriormente):

   ```bash
   docker-compose run --rm webserver airflow db init
   ```

### Conclusão

A correção principal é garantir que o contêiner do Docker tenha permissão para acessar as pastas locais, como `logs`, `dags` e `plugins`. Após ajustar as permissões e reiniciar os serviços, o erro deve ser resolvido. Se precisar de mais alguma orientação ou tiver outros erros, posso ajudar a solucionar.

# Caso você não consiga realizar o login no Airflo
O login e senha padrão do **Apache Airflow** ao acessar a interface web pela primeira vez (especialmente quando configurado com o Docker Compose) costumam ser:

- **Usuário**: `airflow`
- **Senha**: `airflow`

### Caso você queira criar um novo usuário administrador
Se as credenciais padrão não funcionarem ou você quiser criar um novo usuário com permissões de administrador, você pode rodar o seguinte comando para criar um usuário:

1. Execute o comando dentro do contêiner `webserver` para criar um novo usuário administrador:

   ```bash
   docker-compose run --rm webserver airflow users create \
     --username meu_usuario \
     --firstname meu_nome \
     --lastname meu_sobrenome \
     --role Admin \
     --email meu_email@example.com \
     --password minha_senha
   ```

   Esse comando irá criar um novo usuário com o nome de usuário, senha e email que você definir. 

Após isso, você poderá usar as novas credenciais para acessar o Airflow na interface web.

No próximo post vou ensinar como criar a sua primeira Dag!