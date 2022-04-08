---
layout: post
title:  "Como configurar o Apache Spark"
date:   2022-03-14 15:28:03 -0300
categories: spark big-data
---

![Apache Spark]({{ site.url }}/assets/apache-spark.png){:style="width: 100%" }


E aí dev blz? No post de hoje vamos trocar aquela ideia marota sobre uma das tecnologias mais utilizadas em ambiente de Big-Data no mercado de trabalho por empresas nacionais e multi-nacionais.

## O que é o Apache Spark?

O Apache Spark é uma engine (i.e., componente de big data escalável) utilizado em processos de engenharia de dados, data science e machine learning que pode ser utilizado por uma única máquina ou por um conjunto de máquinas (i.e., cluster). Em geral você irá encontrar o SPARK sendo muito utilizado na construção de pipelines de dados.

Algumas features que acompanham o Apache Spark:

__Batch/streaming data__:
* Com Apache Spark você pode realizar processamento de dados em batch (i.e., em lote) ou em tempo real (real-time/streaming). Você pode fazer esse processamento usando a linguagem: Python, SQL, Scala (nativa do SPARK), Java ou R.

__SQL Analytics__:
* Executar de forma rápida e simples consultas de ANSI __SQL__ assim como já faz em ambiente relacional tradicional voltado para construção de dashboards analíticos. Execução de consultas mais rápidas do que em ambientes data warehouses tradicionais. 

__Data Science em larga scala__:
* Realizar análise exploratória de dados (i.e., Exploratory Data Analysis (EDA)) de maneira performática sobre __petabytes__ de dados.

__Machine learning__:
* Possibilidade de treinar os mesmo algoritmos de machine learning que você utiliza no seu laptop pessoal só que em larga escala, em ambiente tolerante a falhas e utilizando centenas de máquinas a seu favor com a possibilidade melhorar sua performance de acordo com a sua necessidade.

Borá aprender como brincar com essa tecnologia no nosso computador que temos em casa.

## Como configurar o Apache Spark

Para configurar o Apache Spark no nosso computador pessoal precisamos ter alguns elementos sendo eles:
* JAVA
* SPARK
* winutils.exe (i.e., para o caso de você estar utilizando um computador com sistema operacional windows)

Não se preocupe pois vou te mostrar como é simples fazer isso ok!

Vamos começar pelo JAVA:

Primeiramente você precisa ter instalado na sua máquina o Java 8 ou superior (JDK).

__Sistema Operacional Windows: Instalando e configurando o JAVA__:
- __Forma simples e rápida__:
    * Você pode fazer o download do JDK no link -> [clique aqui!](https://www.azul.com/downloads/?package=jdk). 
        * Instale o zulu openjdk versão 8 ou superior para o windows usando o arquivo '.msi':
            - Para instalar o zulu openjdk versão 8 ou superior para windows utilizando o arquivo '.msi' é muito simples, basta dar um clique duplo no arquivo que você baixou do site no link acima e seguir as instruções até completar o processo.

- __Forma manual e não tão simples para devs iniciantes__:
    * Instalando o openjdk no Windows utilizando o arquivo comprimido com extensão .zip do Zulu encontrado no link -> [clique aqui!](https://www.azul.com/downloads/?package=jdk);
    * Depois de baixar o arquivo mencionado acima, extraia o seu conteúdo para uma pasta do seu computador. Por exemplo, algo como em: 'C:\Program Files\Zulu'. Para isso utilize alguma ferramenta de descompressão  de arquivos nesse caso algo como __Unzip__ ou __Winrar__ ou outra que você saiba utilizar. Depois de extrair o conteúdo do arquivo .zip você precisar mover a pasta extraída para o diretório que você criou anteriormente. Por exemplo: 'C:\Program Files\Zulu\zulu{versão escolhida}-jdk{versão escolhida}-win_x64' você tera algo similar a isso na sua máquina.

- __Configurar o Java para ser reconhecido em todos locais do seu computador caso isso ainda não tenha acontecido__:
    * Para isso acontecer você precisa criar uma __variável de ambiente__ para o Java e adicionar à variável ao Path do sistema:
        - Para fazer isso você precisa fazer o seguinte:
            * Vá para a barra de pesquisa do windows e procure por Variável de Sistema;
            * Clique em adicionar nova ou algo similar a isso;
            * Com a opção de criar uma nova váriavel você irá:
                1. Para nossa váriavel você irá dar o nome: __JAVA_HOME__;
                2. Para o contéudo dela você irá passar o caminho: 'C:\Program Files\Zulu\zulu{versão escolhida}-jdk{versão escolhida}-win_x64' que é a pasta com o jdk 8 ou superior que nós baixamos;
                3. Finalize o processo e pode fechar o gerenciador de variável de sistema do windows.
            * Feito isso abra o seu prompt de comando do windows mais conhecido como CMD e execute o comando:
                java -version
            * Se tudo ocorreu bem você verá uma mensagem ou algo similar a isso como resultado:
                ```bash
                openjdk version "{versão escolhida do jdk}"
                OpenJDK Runtime Environment (build {versão escolhida do jdk}
                OpenJDK 64-Bit Server VM (build {versão escolhida do jdk}-Nome do seu Sistema Operacional, mixed mode, sharing)
                ```
            * Parabéns se você conseguiu fazer tudo isso, agora você já tem o JAVA configurado na sua máquina para o desenvolvimento de software que vamos precisar!

Se você tem um conhecimento razoavel de inglês para leitura você também pode se guiar por meio da documentação oficial do Zulu para o windows clicando no link -> [clique aqui!](https://docs.azul.com/core/zulu-openjdk/install/windows).


__Sistema Operacional Linux (Ubuntu): Instalando e configurando o JAVA__:

__Forma simples e rápida__:
Para iniciarmos a instalação do Java vamos precisar utilizar o PPA do WebUpd8.

Let's bora devs!:
* Abra o terminal e informe o repositório digitando o comando a seguir:
```bash
sudo add-apt-repository ppa:webupd8team/java
```
* Agora vamos atualizar a base de dados e para isso ainda no terminal digite:
```bash
   sudo apt update 
```
* Para instalar o Java 8 digite no terminal:
```bash
 sudo apt install oracle-java8-installer
```
* Depois verificar se o Java foi instalado corretamente digitando no terminal o comando:
```bash
 java -version
```
Se tudo deu certo o resultado será algo similar a esse:
```bash
"java version "1.8.0_101"
Java(TM) SE Runtime Environment (build 1.8.0_101-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode"
```
O exemplo acima eu apresentei como fazer isso para o JAVA fornecido pela oracle. Se você quiser fazer utilizando o Zulu assim como fiz para o windows você pode fazer por meio da documentação oficial do Zulu clicando no link -> [clique aqui!](https://docs.azul.com/core/zulu-openjdk/install/debian). 

Você apenas precisa se atentar para qual versão está instalando blz. Se ainda tiver dúvidas digita ai nos comentários no final da página que nós tentaremos te ajudar blz.


__Com isso terminamos a configuração do JAVA!__

Agora, a partir dessa parte vamos começar o processo de configuração do Apache Spark.



