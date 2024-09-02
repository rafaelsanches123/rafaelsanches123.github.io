---
layout: post
title:  "O que é Apache Kafka?"
date:   2024-09-01 00:00:00 -0300
categories: data data-analytics data-architecture arquitetura-de-dados apache kafka streaming analytics
---

![Dados Mestres]({{ site.url }}/assets/apache-kafka.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post vou ensinar para vocês o que é Apache Kafka essa ferramenta poderosa para processar, analisar e agir sobre grandes quantidades de dados em tempo real.

Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

# __O que é Apache Kafka ?__

O Apache Kafka é uma plataforma de streaming de eventos distribuída e de código aberto, criada pela Apache Software Foundation. Ele é usado principalmente para construir pipelines de dados em tempo real e aplicativos de streaming de dados. Originalmente desenvolvido pela LinkedIn, o Kafka foi projetado para lidar com grandes volumes de dados e facilitar a troca de mensagens entre diferentes sistemas.

### Principais conceitos e características do Kafka:

1. **Streams (Fluxos de Dados)**: O Kafka permite que os dados sejam publicados e subscritos em tempo real em tópicos, que são essencialmente canais de comunicação. Os produtores (produtores) enviam dados para esses tópicos, enquanto os consumidores (consumidores) lêem os dados desses tópicos.

2. **Tópicos**: Os dados no Kafka são organizados em tópicos. Cada tópico é dividido em várias partições, que permitem que os dados sejam distribuídos e paralelizados.

3. **Escalabilidade**: O Kafka é altamente escalável. Ele pode manipular um grande número de eventos em tempo real, distribuindo as partições dos tópicos em múltiplos servidores, conhecidos como brokers.

4. **Persistência**: O Kafka armazena dados de forma durável, o que significa que as mensagens podem ser persistidas em disco por um determinado período, configurável pelo usuário.

5. **Baixa Latência e Alta Taxa de Transferência**: Projetado para entregar dados com alta taxa de transferência e baixa latência, o Kafka é adequado para sistemas que exigem processamento rápido de grandes volumes de dados.

6. **Processamento de Fluxos**: Além de ser uma plataforma de mensageria, o Kafka oferece a API Kafka Streams, que permite o processamento de dados em tempo real, possibilitando transformar, agregar e manipular os dados à medida que eles fluem através dos tópicos.

### Usos Comuns do Kafka:

- **Integração de Sistemas**: Conectar diferentes aplicativos que precisam trocar dados em tempo real.
- **Monitoramento e Análise em Tempo Real**: Coletar e processar logs ou eventos de sistemas em tempo real.
- **Pipelines de Dados**: Construir pipelines de dados para ingestão e processamento de grandes volumes de dados.
- **Plataformas de Streaming**: Criar plataformas de dados em tempo real, como recomendações de conteúdo e análises de redes sociais.

Em resumo, o Apache Kafka é uma ferramenta poderosa para empresas que precisam processar, analisar e agir sobre grandes quantidades de dados em tempo real, como recomendações de conteúdo e análises de redes sociais.

# __Arquitetura do Apache Kafka__

A arquitetura do Apache Kafka é projetada para ser escalável, resiliente e eficiente no processamento de fluxos de dados em tempo real. Ela é composta por vários componentes-chave que trabalham juntos para permitir a publicação, o armazenamento e o consumo de mensagens de maneira distribuída. Aqui estão os principais componentes e conceitos da arquitetura do Kafka:

### 1. **Tópicos**
- **Definição**: Os tópicos são os canais de comunicação no Kafka. Cada tópico é um stream de dados onde as mensagens são publicadas pelos produtores e consumidas pelos consumidores.
- **Partições**: Um tópico é dividido em várias partições, que são unidades menores e ordenadas de mensagens. As partições permitem que os dados sejam distribuídos entre vários brokers, aumentando a escalabilidade.
- **Ordenação**: Dentro de uma partição, as mensagens são ordenadas de forma imutável, e cada mensagem recebe um número único chamado "offset", que representa a posição dessa mensagem dentro da partição.

### 2. **Brokers**
- **Definição**: Um broker é uma instância do Kafka que gerencia a persistência e o envio de mensagens para os consumidores. Em uma configuração típica, você terá um cluster de múltiplos brokers para aumentar a resiliência e a capacidade de processamento.
- **Distribuição**: As partições de um tópico são distribuídas entre os brokers, o que significa que diferentes partes do mesmo tópico podem ser armazenadas em diferentes brokers.
- **Replicação**: Para garantir a alta disponibilidade, as partições podem ser replicadas entre brokers. Cada partição tem um líder (que processa todas as operações de leitura e gravação) e réplicas, que ficam disponíveis caso o líder falhe.

### 3. **Produtores (Producers)**
- **Definição**: Os produtores são responsáveis por enviar dados para os tópicos no Kafka. Eles podem escolher para qual partição enviar a mensagem, muitas vezes usando uma chave para garantir que todas as mensagens com a mesma chave sejam enviadas para a mesma partição.
- **Função**: Produtores enviam dados para os brokers, e o Kafka garante a persistência e distribuição desses dados.

### 4. **Consumidores (Consumers)**
- **Definição**: Os consumidores são aplicativos que leem dados de um ou mais tópicos no Kafka.
- **Grupos de Consumidores (Consumer Groups)**: Consumidores podem se agrupar em "consumer groups". Cada partição de um tópico é consumida por apenas um consumidor dentro de um grupo, o que significa que, se você tiver mais consumidores do que partições, alguns consumidores ficarão inativos.
- **Controle de Offset**: Os consumidores podem controlar qual offset ler, permitindo a leitura de mensagens desde um determinado ponto ou repetir leituras se necessário.

### 5. **Zookeeper**
- **Definição**: O Zookeeper é usado pelo Kafka para manter informações de configuração e coordenação entre os brokers. Ele rastreia o status dos brokers e dos tópicos no cluster.
- **Função**: Embora o Kafka dependa do Zookeeper para gerenciamento de estado, com as versões mais recentes do Kafka (a partir da 2.8), há uma transição para um novo modo de gerenciamento interno de metadados, permitindo a operação sem Zookeeper.

### 6. **Log de Partições**
- **Persistência**: Cada partição é implementada como um log que armazena as mensagens em disco de maneira sequencial. Isso permite que o Kafka seja extremamente eficiente em termos de E/S (entrada e saída).
- **Retenção**: As mensagens podem ser mantidas no log por um período configurável, independentemente de terem sido consumidas ou não. Isso significa que diferentes consumidores podem ler as mesmas mensagens em momentos diferentes.

### 7. **Replicação e Tolerância a Falhas**
- **Replicação**: Como mencionado anteriormente, as partições podem ser replicadas para garantir a alta disponibilidade. Se o broker que hospeda a partição líder falhar, uma das réplicas assumirá automaticamente.
- **Resiliência**: O Kafka é projetado para continuar funcionando mesmo com falhas de hardware, graças à sua replicação e à natureza distribuída dos brokers e partições.

### 8. **Kafka Streams e Kafka Connect**
- **Kafka Streams**: Uma API que permite o processamento de fluxos de dados diretamente no Kafka. Ele facilita a transformação, agregação e análise de dados em tempo real.
- **Kafka Connect**: Um framework que simplifica a integração do Kafka com outros sistemas, como bancos de dados, sistemas de armazenamento em nuvem e sistemas de monitoramento.

### Resumo Visual

Em construção...

### Considerações finais referentes a arquitetura do kafka
A arquitetura do Apache Kafka é construída para suportar grandes volumes de dados, fornecer alta disponibilidade e garantir a integridade dos dados através de sua replicação e gerenciamento de partições. Ele é ideal para sistemas que exigem processamento de dados em tempo real e escalabilidade horizontal.

# __Instalação e comando básicos__

A instalação e configuração do Apache Kafka no Linux Ubuntu envolve várias etapas. Vou guiá-lo pelo processo de instalação e configuração básica para começar a usar o Kafka.

### Passo 1: Atualizar os pacotes do sistema
Antes de instalar qualquer software, é uma boa prática atualizar os pacotes do sistema:

```bash
sudo apt-get update
sudo apt-get upgrade -y
```

### Passo 2: Instalar o Java
O Apache Kafka requer o Java para ser executado. Instale o OpenJDK (Java Development Kit) com o comando:

```bash
sudo apt-get install default-jdk -y
```

### Passo 3: Verificar a versão do Java
Certifique-se de que o Java está instalado corretamente:

```bash
java -version
```

Isso deve retornar a versão do Java instalada, confirmando que o Java está pronto para uso.

### Passo 4: Baixar e extrair o Apache Kafka
Acesse o site oficial do Apache Kafka ou baixe a versão mais recente diretamente via terminal:

```bash
wget https://downloads.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz
```

Extraia o arquivo baixado:

```bash
tar -xzf kafka_2.13-3.0.0.tgz
```

Renomeie o diretório para facilitar o acesso:

```bash
mv kafka_2.13-3.0.0 kafka
```

### Passo 5: Configurar o Apache Kafka
O Kafka depende do Zookeeper para gerenciar e coordenar os brokers. O Zookeeper já vem incluído no pacote Kafka.

Primeiro, inicie o Zookeeper:

```bash
cd kafka
bin/zookeeper-server-start.sh config/zookeeper.properties
```

Em outro terminal, inicie o Kafka:

```bash
bin/kafka-server-start.sh config/server.properties
```

Agora, o Kafka está em execução, com um broker padrão configurado.

### Passo 6: Testar a instalação do Kafka
Vamos criar um tópico, enviar mensagens para ele e consumir essas mensagens para garantir que tudo está funcionando corretamente.

1. **Criar um Tópico**:

   ```bash
   bin/kafka-topics.sh --create --topic test --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
   ```

2. **Listar Tópicos**:

   ```bash
   bin/kafka-topics.sh --list --bootstrap-server localhost:9092
   ```

   Isso deve mostrar o tópico `test` que você acabou de criar.

3. **Produzir Mensagens para o Tópico**:

   ```bash
   bin/kafka-console-producer.sh --topic test --bootstrap-server localhost:9092
   ```

   Digite algumas mensagens e pressione `Enter` após cada uma.

4. **Consumir Mensagens do Tópico**:

   Em outro terminal, execute:

   ```bash
   bin/kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092
   ```

   Isso deve exibir as mensagens que você digitou anteriormente.

### Passo 7: Parar o Kafka e o Zookeeper
Quando terminar de usar o Kafka, pare os servidores Kafka e Zookeeper:

1. **Parar o Kafka**:

   ```bash
   bin/kafka-server-stop.sh
   ```

2. **Parar o Zookeeper**:

   ```bash
   bin/zookeeper-server-stop.sh
   ```

### Conclusão
Você instalou e configurou o Apache Kafka no Ubuntu com sucesso. Agora, pode explorar suas funcionalidades para criar sistemas de processamento de dados em tempo real.
