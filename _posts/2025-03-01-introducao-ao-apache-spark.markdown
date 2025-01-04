---
layout: post
title:  "Introdução ao Apache Spark"
date:   2025-01-03 00:00:01 -0300
categories: 
---

![Spark]({{ site.url }}/assets/apache-spark.png){:style="width: 100%" }

Em um mundo movido por dados, o processamento eficiente e rápido de grandes volumes de informações se tornou essencial. É nesse cenário que o **Apache Spark** se destaca como uma das ferramentas mais poderosas e versáteis para o processamento distribuído de dados. Desde o processamento em lote até o streaming em tempo real, o Spark é amplamente utilizado por empresas para lidar com desafios de **big data**.

Neste post, vamos explorar como você pode configurar o Apache Spark no seu ambiente e começar a trabalhar com ele usando **PySpark**, a interface Python do Spark. Além disso, apresentarei um exemplo prático onde utilizaremos o Spark para processar um arquivo CSV, calcular métricas importantes e visualizar os resultados. Se você está buscando uma introdução clara e prática para essa tecnologia, veio ao lugar certo!

Pronto para descobrir o que faz do Apache Spark uma peça-chave no ecossistema de dados moderno? Vamos começar!

O Apache Spark é uma plataforma de processamento de dados de código aberto, projetada para processar grandes volumes de dados (big data) de maneira distribuída e em alta velocidade. Ele foi desenvolvido no laboratório AMPLab da Universidade de Berkeley e lançado pela primeira vez em 2010. Desde então, tornou-se uma das tecnologias mais populares para análise de dados em grande escala.

---

### **O que é o Apache Spark?**
O Spark é uma **engine unificada** para processamento de dados distribuído que pode lidar com várias tarefas, como processamento em lote, análise em tempo real, aprendizado de máquina e consultas interativas. Ele utiliza clusters de computadores para processar dados de forma paralela, o que garante maior eficiência e velocidade em relação a outras tecnologias, como o Hadoop MapReduce.

---

### **Principais características**
- **Rápido:** O Spark é projetado para ser significativamente mais rápido do que o Hadoop MapReduce devido à sua capacidade de manter os dados na memória (in-memory processing). Ele só grava no disco quando necessário, reduzindo a latência.
  
- **Fácil de usar:** Suporta APIs de alto nível em várias linguagens, como Python (PySpark), Scala, Java e R, o que o torna acessível para desenvolvedores de diferentes backgrounds.

- **Versátil:** Ele suporta diferentes tipos de processamento de dados, como:
  - **Processamento em lote** (batch processing) para grandes volumes de dados históricos.
  - **Streaming em tempo real** (real-time processing) para fluxos de dados contínuos.
  - **Machine Learning (MLlib):** Possui bibliotecas nativas para aprendizado de máquina.
  - **SQL:** Permite executar consultas SQL sobre os dados.
  - **Graph Processing (GraphX):** Para análise de grafos.

- **Distribuído:** O Spark distribui o processamento entre vários nós em um cluster, garantindo alta escalabilidade e resiliência.

---

### **Arquitetura do Apache Spark**
A arquitetura do Spark é composta por dois elementos principais: **Driver** e **Executors**.

#### **Componentes principais**
1. **Driver Program:** O driver é responsável por orquestrar a execução do programa. Ele distribui tarefas aos executores e coleta os resultados. O código do usuário é enviado ao driver.

2. **Cluster Manager:** É o gerenciador de recursos do cluster. O Spark pode usar diferentes gerenciadores, como:
   - Standalone (nativo do Spark)
   - Hadoop YARN
   - Kubernetes
   - Mesos

3. **Executors:** São processos distribuídos que executam as tarefas atribuídas pelo driver. Cada executor processa uma parte dos dados e mantém uma parte da memória reservada para o cache.

4. **RDDs (Resilient Distributed Datasets):** Os RDDs são a principal abstração do Spark para representar dados distribuídos em um cluster. Eles são tolerantes a falhas e permitem transformações imutáveis, como map e filter.

---

### **Principais bibliotecas e módulos do Spark**
O Spark oferece um ecossistema rico com bibliotecas integradas:

1. **Spark Core:**
   - O núcleo do Spark, que fornece APIs básicas e suporte para RDDs.

2. **Spark SQL:**
   - Suporte para consultas SQL e integração com fontes de dados estruturados, como bancos de dados relacionais e Apache Hive.

3. **Spark Streaming:**
   - Permite o processamento de dados em tempo real, como logs ou eventos.

4. **MLlib (Machine Learning Library):**
   - Oferece algoritmos para aprendizado de máquina, como regressão, clustering e recomendações.

5. **GraphX:**
   - Ferramenta para processamento e análise de grafos, como redes sociais ou mapas.

---

### **Casos de uso**
O Apache Spark é utilizado em uma ampla variedade de setores e casos de uso, incluindo:

- **Processamento de logs:** Empresas usam o Spark para analisar logs de servidores ou aplicativos para monitoramento e solução de problemas.
- **Análise de redes sociais:** Processar e analisar grandes volumes de dados de redes sociais.
- **Ciência de dados e aprendizado de máquina:** Treinamento de modelos de IA com grandes volumes de dados usando MLlib.
- **Análise de dados financeiros:** Processamento de transações financeiras para detectar fraudes em tempo real.
- **Bioinformática:** Análise de grandes volumes de dados genômicos.

---

### **Comparação com o Hadoop**
O Apache Spark é frequentemente comparado ao Hadoop, pois ambos são tecnologias para processamento distribuído. Algumas diferenças importantes:

| Característica         | Apache Spark                  | Hadoop MapReduce            |
|------------------------|------------------------------|-----------------------------|
| **Velocidade**         | Processamento na memória     | Baseado em disco            |
| **Facilidade de uso**  | APIs mais simples e expressivas | Mais complexo               |
| **Versatilidade**      | Suporte nativo a SQL, ML, streaming | Processamento em lote apenas |
| **Comunidade**         | Comunidade crescente         | Bem estabelecida            |

Se não sabe o que é o Hadoop recomendo a leitura: [Introdução a Arquitetura Hadoop]({%  link _posts/2021-05-25-introducao-a-arquitetura-hadoop.markdown %}).

---

A seguir vou te apresentar 3 formas de usar o Apache Spark sendo elas:
* Localmente instalado e configurado na sua máquina;
* Localmente usando docker + docker compose já ensinados aqui no blog;
* Online usando Google Colab.

---

## **1° Localmente instalado na sua máquina**:

### **1. Configurando o Apache Spark no Linux Ubuntu ou versões derivadas dele e do Debian**

A configuração do Apache Spark depende do seu ambiente, mas vou cobrir os passos básicos para configurá-lo localmente, seguido de um exemplo prático.

### **Passo 1: Instalar dependências**
Antes de instalar o Spark, você precisa de:
- **Java JDK (Java Development Kit):** O Spark requer o JDK para funcionar.
  - Verifique se está instalado:  
    ```bash
    java -version
    ```
  - Caso não esteja, instale-o (ex.: OpenJDK 11):
    ```bash
    sudo apt update
    sudo apt install openjdk-11-jdk
    ```

- **Python:** Para usar PySpark, você precisa de Python instalado.
  - Verifique a instalação:  
    ```bash
    python3 --version
    ```

- **Apache Spark:** Baixe a versão mais recente do [site oficial do Apache Spark](https://spark.apache.org/downloads.html).
  - Escolha a versão desejada e o pacote Hadoop apropriado (se não usar Hadoop, escolha o pré-empacotado com `Hadoop-free`).

### **Passo 2: Configurar variáveis de ambiente**
Após o download, extraia o arquivo compactado e configure as variáveis de ambiente.

1. Extraia o Spark:
   ```bash
   tar -xvzf spark-<versao>.tgz
   mv spark-<versao> /opt/spark
   ```

2. Adicione o Spark ao `PATH` no arquivo `~/.bashrc` ou `~/.zshrc`:
   ```bash
   export SPARK_HOME=/opt/spark
   export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
   ```

3. Atualize o terminal:
   ```bash
   source ~/.bashrc
   ```

4. Verifique a instalação:
   ```bash
   spark-shell
   ```
   Isso abrirá o shell do Spark, confirmando que está funcionando.

### **Passo 3: Instalar o PySpark**
Para usar PySpark com Python:
```bash
pip install pyspark
```

---

## **2. Exemplo prático com PySpark**

Agora que o Spark está configurado, vamos criar um exemplo prático para processar dados com PySpark.

### **Cenário**
Vamos processar um arquivo CSV com informações de vendas e calcular a receita total por produto.

### **Dataset de exemplo (vendas.csv)**:
Salve este conteúdo em um arquivo `vendas.csv`:
```csv
produto,quantidade,preco
Laptop,2,2000
Mouse,5,50
Teclado,3,100
Monitor,1,500
Laptop,1,2000
Mouse,2,50
```

### **Código em Python (PySpark)**:
Crie um arquivo Python `processa_vendas.py` com o seguinte código:

```python
from pyspark.sql import SparkSession

# 1. Criar a sessão Spark
spark = SparkSession.builder \
    .appName("Processamento de Vendas") \
    .getOrCreate()

# 2. Carregar o arquivo CSV no DataFrame
arquivo_csv = "vendas.csv"
vendas_df = spark.read.csv(arquivo_csv, header=True, inferSchema=True)

# 3. Exibir o DataFrame carregado
print("Dados carregados:")
vendas_df.show()

# 4. Calcular a receita total por produto
vendas_df = vendas_df.withColumn("receita", vendas_df["quantidade"] * vendas_df["preco"])
receita_total = vendas_df.groupBy("produto").sum("receita")

# 5. Renomear coluna e exibir o resultado
receita_total = receita_total.withColumnRenamed("sum(receita)", "receita_total")
print("Receita total por produto:")
receita_total.show()

# 6. Finalizar a sessão Spark
spark.stop()
```

### **Passo a passo do código**
1. **Criar a sessão Spark:** O `SparkSession` é a entrada principal para PySpark.
2. **Carregar o CSV:** Usamos `spark.read.csv` para carregar o arquivo como um DataFrame.
3. **Exibir os dados:** `DataFrame.show()` imprime os dados no terminal.
4. **Calcular a receita total:** Criamos uma nova coluna `receita` e agrupamos os dados por `produto`.
5. **Renomear e exibir:** Modificamos os nomes das colunas para facilitar a leitura e exibimos o resultado.

### **Executar o script**
Certifique-se de que o `vendas.csv` está no mesmo diretório que o script e execute:
```bash
python3 processa_vendas.py
```

---

## **3. Saída esperada**
A saída no terminal será algo como:

**Dados carregados:**
```
+--------+----------+-----+
| produto|quantidade|preco|
+--------+----------+-----+
|  Laptop|         2| 2000|
|   Mouse|         5|   50|
| Teclado|         3|  100|
| Monitor|         1|  500|
|  Laptop|         1| 2000|
|   Mouse|         2|   50|
+--------+----------+-----+
```

**Receita total por produto:**
```
+--------+-------------+
| produto|receita_total|
+--------+-------------+
|  Laptop|         6000|
|   Mouse|          350|
| Teclado|          300|
| Monitor|          500|
+--------+-------------+
```

---

## **4. Próximos passos**
Se você quiser expandir este exemplo, podemos:
- Adicionar integração com outras fontes de dados, como bancos de dados ou APIs.
- Criar visualizações com bibliotecas Python (ex.: Matplotlib ou Seaborn).
- Trabalhar com aprendizado de máquina usando o **MLlib** do Spark.

Quer explorar algo específico no PySpark ou outras ferramentas relacionadas? 😊 Me fala nos comentários e bora aprender juntos!

---
---

## **2° Localmente usando docker + docker compose já ensinados aqui no blog**:


## **1. Configurando o ambiente com Docker Compose**

Vamos criar um ambiente com o Spark em contêineres usando [Docker Compose]({% link _posts/2024-12-18-instalando-docker-compose.markdown %}). Isso simplifica o processo de configurar o Spark localmente e é ideal para cenários de teste ou desenvolvimento.

### **Passo 1: Criar o arquivo `docker-compose.yml`**

Crie um arquivo chamado `docker-compose.yml` com o seguinte conteúdo:

```yaml
version: "3.9"
services:
  spark-master:
    image: bitnami/spark:latest
    container_name: spark-master
    hostname: spark-master
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_DIRS=/tmp/spark
    ports:
      - "8080:8080" # UI do Spark
      - "7077:7077" # Porta do cluster
    networks:
      - spark-network

  spark-worker:
    image: bitnami/spark:latest
    container_name: spark-worker
    hostname: spark-worker
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark-master:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
    depends_on:
      - spark-master
    networks:
      - spark-network

  pyspark:
    image: bitnami/spark:latest
    container_name: pyspark
    hostname: pyspark
    environment:
      - SPARK_MODE=client
      - SPARK_MASTER_URL=spark://spark-master:7077
    volumes:
      - ./app:/app
    working_dir: /app
    depends_on:
      - spark-master
    networks:
      - spark-network
    command: tail -f /dev/null

networks:
  spark-network:
    driver: bridge
```

### **Passo 2: Estrutura do projeto**
Organize os arquivos no seguinte formato:

```
/projeto-spark
│
├── docker-compose.yml
├── app/
    ├── vendas.csv
    └── processa_vendas.py
```

- **`docker-compose.yml`**: Configura o ambiente Docker.
- **`vendas.csv`**: Arquivo de entrada de dados.
- **`processa_vendas.py`**: Script PySpark para processar os dados.

### **Passo 3: Adicionar o código PySpark**

Coloque o seguinte código no arquivo `app/processa_vendas.py`:

```python
from pyspark.sql import SparkSession

# Criar a sessão Spark
spark = SparkSession.builder \
    .appName("Processamento de Vendas") \
    .getOrCreate()

# Carregar o arquivo CSV no DataFrame
arquivo_csv = "vendas.csv"
vendas_df = spark.read.csv(arquivo_csv, header=True, inferSchema=True)

# Exibir o DataFrame carregado
print("Dados carregados:")
vendas_df.show()

# Calcular a receita total por produto
vendas_df = vendas_df.withColumn("receita", vendas_df["quantidade"] * vendas_df["preco"])
receita_total = vendas_df.groupBy("produto").sum("receita")

# Renomear coluna e exibir o resultado
receita_total = receita_total.withColumnRenamed("sum(receita)", "receita_total")
print("Receita total por produto:")
receita_total.show()

# Finalizar a sessão Spark
spark.stop()
```

---

## **2. Executando o ambiente com Docker Compose**

### **Passo 1: Subir os contêineres**
No diretório onde está o `docker-compose.yml`, execute no terminal:

```bash
docker-compose up -d
```

Isso iniciará o **master**, **worker** e o contêiner do cliente **pyspark**.

### **Passo 2: Acessar o contêiner PySpark**
Conecte-se ao contêiner `pyspark`:

```bash
docker exec -it pyspark bash
```

Dentro do contêiner, verifique os arquivos no diretório `/app`:

```bash
ls /app
```

Você verá os arquivos `processa_vendas.py` e `vendas.csv`.

### **Passo 3: Executar o script PySpark**
Dentro do contêiner, execute o script:

```bash
spark-submit processa_vendas.py
```

---

## **3. Resultado esperado**

A saída será semelhante a:

**Dados carregados:**
```
+--------+----------+-----+
| produto|quantidade|preco|
+--------+----------+-----+
|  Laptop|         2| 2000|
|   Mouse|         5|   50|
| Teclado|         3|  100|
| Monitor|         1|  500|
|  Laptop|         1| 2000|
|   Mouse|         2|   50|
+--------+----------+-----+
```

**Receita total por produto:**
```
+--------+-------------+
| produto|receita_total|
+--------+-------------+
|  Laptop|         6000|
|   Mouse|          350|
| Teclado|          300|
| Monitor|          500|
+--------+-------------+
```

---

## **4. Encerrando os contêineres**
Após terminar, desligue o ambiente com:

```bash
docker-compose down
```

---

Com este setup, você pode facilmente reutilizar o ambiente Spark para outros experimentos. Que tal? 😊 Me fala nos comentários o que achou!

---
---

## **3° Online usando Google Colab**:

Utilizar o **Apache Spark** no **Google Colab** é uma excelente alternativa para quem deseja __explorar o Spark sem precisar configurar um ambiente local__. Aqui está o passo a passo para configurar e executar o Spark no Colab.

---

## **1. Configurando o Spark no Google Colab**

### **Passo 1: Instalar dependências**
No Google Colab, execute o seguinte código em uma célula para instalar o Spark e o Java (necessário para o Spark):

```python
!apt-get install openjdk-11-jdk-headless -qq > /dev/null
!wget -q https://downloads.apache.org/spark/spark-3.5.0/spark-3.5.0-bin-hadoop3.tgz
!tar xf spark-3.5.0-bin-hadoop3.tgz
!pip install -q findspark
```

- **`openjdk-11-jdk-headless`**: Instala o Java necessário para o Spark.
- **Spark 3.5.0**: Você pode alterar o link para outra versão, se necessário.
- **`findspark`**: Facilita a integração do Spark com o Python no Colab.

### **Passo 2: Configurar variáveis de ambiente**
Após a instalação, configure as variáveis de ambiente no Colab para que o Python reconheça o Spark:

```python
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-11-openjdk-amd64"
os.environ["SPARK_HOME"] = "/content/spark-3.5.0-bin-hadoop3"
```

### **Passo 3: Iniciar o Spark no Colab**
Agora, inicialize o Spark com a biblioteca `findspark`:

```python
import findspark
findspark.init()

from pyspark.sql import SparkSession

# Criar uma sessão Spark
spark = SparkSession.builder \
    .appName("Spark no Google Colab") \
    .getOrCreate()

print("Sessão Spark inicializada!")
```

Se tudo estiver configurado corretamente, você verá a mensagem **"Sessão Spark inicializada!"**.

---

## **2. Exemplo prático com Spark no Colab**

Vamos usar o mesmo exemplo de processamento de um arquivo CSV, como no exemplo anterior.

### **Passo 1: Criar um arquivo CSV no Colab**
Crie o arquivo `vendas.csv` diretamente no Colab:

```python
data = """produto,quantidade,preco
Laptop,2,2000
Mouse,5,50
Teclado,3,100
Monitor,1,500
Laptop,1,2000
Mouse,2,50"""

with open("vendas.csv", "w") as file:
    file.write(data)
```

Isso cria o arquivo **vendas.csv** no diretório atual.

---

### **Passo 2: Processar o CSV com PySpark**
Agora, use o PySpark para processar os dados, calcular a receita total por produto e exibir os resultados:

```python
# Carregar o arquivo CSV no DataFrame
vendas_df = spark.read.csv("vendas.csv", header=True, inferSchema=True)

# Exibir os dados carregados
print("Dados carregados:")
vendas_df.show()

# Calcular a receita total
from pyspark.sql.functions import col

vendas_df = vendas_df.withColumn("receita", col("quantidade") * col("preco"))
receita_total = vendas_df.groupBy("produto").sum("receita")

# Renomear a coluna e exibir o resultado
receita_total = receita_total.withColumnRenamed("sum(receita)", "receita_total")
print("Receita total por produto:")
receita_total.show()
```

---

## **3. Resultado esperado**

**Dados carregados:**
```
+--------+----------+-----+
| produto|quantidade|preco|
+--------+----------+-----+
|  Laptop|         2| 2000|
|   Mouse|         5|   50|
| Teclado|         3|  100|
| Monitor|         1|  500|
|  Laptop|         1| 2000|
|   Mouse|         2|   50|
+--------+----------+-----+
```

**Receita total por produto:**
```
+--------+-------------+
| produto|receita_total|
+--------+-------------+
|  Laptop|         6000|
|   Mouse|          350|
| Teclado|          300|
| Monitor|          500|
+--------+-------------+
```

---

## **4. Benefícios de usar o Colab para Spark**
- **Sem configuração local:** O Colab fornece um ambiente pré-configurado na nuvem.
- **Facilidade de colaboração:** Compartilhe o notebook com colegas para trabalhar juntos.
- **Integração com bibliotecas Python:** Use outras bibliotecas como Matplotlib ou Pandas facilmente.

Agora que você aprendeu várias maneiras de instalar, configurar e usar o Spark sem precisar instalá-lo diretamente na sua máquina local, desejo muito sucesso nos seus estudos! Lembre-se: quanto mais você praticar, melhor se tornará no uso do Spark.