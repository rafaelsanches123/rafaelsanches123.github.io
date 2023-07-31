---
layout: post
title:  "Introdução a linguagem SQL com Sqlite"
date:   2023-07-23 10:00:00 -0300
categories: sql
---

![SQL]({{ site.url }}/assets/SQL.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre a linguagem de consulta estruturada (SQL). Essa linguagem no momento está sendo bastante difundida no mercado e também está sendo muito requisitada nas vagas de emprego voltadas para a área de DADOS. Para entender os conceitos por trás do SQL vamos utilizar no post de hoje o Sqlite que é um banco de dados relacional leve, simples e super fácil de utilizar para aprender SQL. Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

## SQL

SQL (Structured Query Language) é uma linguagem de programação especializada usada para gerenciar e manipular bancos de dados relacionais. Ele permite que você crie, atualize, consulte e gerencie dados em um banco de dados. O SQL é uma linguagem declarativa, o que significa que você especifica o que deseja fazer com os dados, e não como fazer isso. 

## Principais Conceitos do SQL

*   __CREATE TABLE__: Permite criar uma nova tabela no banco de dados e especificar a estrutura das colunas e suas propriedades.

*   __INSERT INTO__: Utilizado para inserir novos registros (linhas) em uma tabela existente.

*   __SELECT__: É usado para recuperar dados de uma tabela. Você pode filtrar, classificar e agrupar os resultados de acordo com suas necessidades.

*   __UPDATE__: Permite modificar os dados existentes em uma tabela.

*   __DELETE__: Usado para excluir registros de uma tabela.

*   __WHERE__: É uma cláusula usada em conjunto com as instruções __SELECT__, __UPDATE__ e __DELETE__ para especificar condições que os dados devem atender para serem incluídos ou modificados.

*   __ORDER BY__: Utilizado para classificar os resultados de uma consulta em ordem ascendente ou descendente com base em uma ou mais colunas.

*   __GROUP BY__: Permite agrupar os resultados de uma consulta com base nos valores de uma ou mais colunas.

*   __JOIN__: Utilizado para combinar dados de duas ou mais tabelas com base em colunas relacionadas.

Agora vamos explorar alguns __conceitos__ do __SQL__ e como usá-lo com o __SQLite__, que é um __banco de dados__ leve e embutido.

__Exemplos com SQLite__:

SQLite é um banco de dados relacional embutido, rápido e eficiente. Não requer um servidor separado e é adequado para aplicações móveis, aplicativos de desktop e outros projetos que exigem uma solução de banco de dados leve. A seguir, temos alguns exemplos de SQL usando o SQLite:

Primeiro passo será a instalação do SQLite no seu sistema operacional:

Para os sistemas operacionais __Linux__ e __MacOS__ o sqlite já vem instalado com sistema operacional.

Se por ventura você não tiver o SQLite no seu linux abra seu terminal e bora instalar.

Instalação e Configuração do SQLite na sua distro Linux:
*   Use a linha de comando a seguir que seja referente a sua distro linux.
```bash
emerge sqlite3 # Gentoo, Funtoo, ...
sudo apt install sqlite3 # Debian, Ubuntu, Mint, ...
sudo pacman -S sqlite3 # Arch, Manjaro, ...
sudo dnf install sqlite3 # Red Hat, CentOS, Fedora, ...
```

Instalação e Configuração do SQLite no Windows:
1.  Download do Binário:
*   Acesse o site oficial do SQLite em [https://www.sqlite.org/download.html](https://www.sqlite.org/download.html).
*   Role a página para baixo até a seção "Precompiled Binaries for Windows".
*   Baixe o arquivo "sqlite-tools-win32-x86-.zip" (para sistemas de 32 bits) ou "sqlite-tools-win32-x64-.zip" (para sistemas de 64 bits).
2.  Extrair o Arquivo:
*   Após o download, extraia o conteúdo do arquivo ZIP para uma pasta de sua escolha. Por exemplo, você pode extrair para "C:\sqlite".
3.  Configuração do PATH (Opcional):
*   Para executar o SQLite a partir de qualquer local no Prompt de Comando, você pode adicionar o diretório de instalação do SQLite ao PATH do sistema.
*   No Windows 10, vá para "Configurações" -> "Sistema" -> "Sobre" -> "Configurações avançadas do sistema".
*   Clique em "Variáveis de Ambiente" e, na seção "Variáveis do Sistema", encontre a variável "Path" e clique em "Editar".
*   Adicione o caminho do diretório do SQLite (por exemplo, "C:\sqlite") ao final da lista de valores.
4.  Teste da Instalação:
*   Abra o Prompt de Comando (ou PowerShell) e digite "sqlite3" e pressione Enter. Isso iniciará o shell interativo do SQLite.

Antes de começar a colocarmos a mão na massa, primeiro precisamos utilizar alguma ferramenta para trabalhar com o nosso banco de dados e realizar as nossas consultas. Para isso você vai precisar baixar no seu computador o __SQLiteStudio__ que será a ferramenta utilizada para aplicarmos os conceitos a seguir.

[Link do site utilizado para baixar o SQLiteStudio](https://sqlitestudio.pl/)

### Criar nossa base de dados:

Para abrir/criar uma base de dados, basta rodar o comando no seu terminal:
```sql
sqlite3 nome-da-minha-base-de-dados.db
```

Caso seja da sua preferência você pode fazer isso via interface gráfica com o SQLiteStudio:
*   Após a instalação, inicie o SQLiteStudio. Você verá uma janela inicial.
*   No menu "__Database__", clique em "__New Database__".
*   Escolha um local para salvar o arquivo do banco de dados SQLite e defina um nome para o banco de dados com a extensão "__.db__" (por exemplo, "meu_banco_de_dados.db").
*   Clique em "Save".

a partir daqui vamos usar o SQLiteStudio e os comandos utilizados podem ser replicados no terminal caso você queira seguir por esse caminho.

No SQLiteStudio va no menu e clique na opção "Open Sql Editor" ou usar o atalho (ALT+E) e isso irá gerar um espaço em branco para editarmos e criarmos nossos comandos SQL. Para executar nossos comandos você pode clicar no botão "Execute Query" ou usar o atalho (F9) e isso irá executar nossos comandos usando SQLiteStudio.

###  Criar uma tabela:
Antes de fato de criarmos nossas tabelas no nosso banco de dados é importante primeiro entender os tipos/formatos de dados que ele nos permite armazenar e manipular.

No __SQLite__, assim como em outros sistemas de gerenciamento de banco de dados, existem vários tipos de dados que você pode usar para definir os tipos de colunas em suas tabelas. O SQLite oferece suporte a um conjunto básico de tipos de dados padrão, que abrangem diferentes tipos de números, texto, datas e valores binários. A seguir, estão os tipos de dados mais comuns no SQLite:

*   __INTEGER__: É usado para armazenar números inteiros. O SQLite armazena os inteiros como inteiros de 1, 2, 3, 4, 6 ou 8 bytes, dependendo do tamanho necessário.

*   __REAL__ (ou FLOAT): É usado para armazenar números de ponto flutuante (números decimais). O SQLite armazena números reais como um número de ponto flutuante de 8 bytes.

*   __TEXT__ (ou VARCHAR ou CHAR): É usado para armazenar texto, como palavras, frases ou sequências de caracteres. O SQLite permite armazenar até 2^31-1 bytes (ou 2 gigabytes) de texto em uma coluna TEXT.

*   __BLOB__: É usado para armazenar dados binários, como imagens, arquivos, documentos ou qualquer outro tipo de dado binário. O SQLite armazena BLOBs como objetos de tamanho variável.

*   __NULL__: É usado para representar valores nulos, indicando que a coluna não tem valor definido.

*   __NUMERIC__ (ou DECIMAL): É usado para armazenar números com precisão fixa ou números em formato de texto. No SQLite, os valores NUMERIC são armazenados como texto e são convertidos para números quando necessário.

*   __BOOLEAN__: O SQLite não possui um tipo de dados booleano nativo, mas você pode usar __INTEGER__ ou __TEXT__ para representar valores booleanos, onde 0 é falso e 1 é verdadeiro.

*   __DATE__: O SQLite não possui um tipo de dados de data nativo, mas você pode armazenar datas como strings de texto no formato "YYYY-MM-DD" ou como valores numéricos representando o número de dias desde uma data de referência.

*   __TIME__: O SQLite não possui um tipo de dados de hora nativo, mas você pode armazenar horários como strings de texto no formato "HH:MM:SS" ou como valores numéricos representando o número de segundos desde a meia-noite.

*   __DATETIME__: O SQLite não possui um tipo de dados de data e hora nativo, mas você pode combinar os tipos de dados DATE e TIME para armazenar data e hora juntos.

É importante escolher o tipo de dado apropriado para cada coluna de acordo com os requisitos de armazenamento e a natureza dos dados que você deseja armazenar. O SQLite é bastante flexível em relação aos tipos de dados, permitindo que você utilize as combinações mais adequadas para o seu aplicativo ou projeto.

Agora sim já podemos criar nossas tabelas.
Vamos supor que temos duas tabelas: "employees" e "departments". A tabela "employees" armazena informações sobre os funcionários, enquanto a tabela "departments" contém informações sobre os departamentos onde esses funcionários trabalham. Ambas as tabelas têm uma coluna "department_id" que representa a chave estrangeira (i.e., a coluna que contem o campo que relaciona as duas tabelas) relacionada ao departamento em que o funcionário está alocado.

Para criar a Tabela employees execute o seguinte comando:

```sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER,
    department_id INTEGER
);

```
Faça o mesmo para a Tabela departments:

```sql
CREATE TABLE departments (
    id INTEGER PRIMARY KEY,
    name TEXT
);

```
A __PRIMARY KEY__ (chave primária) é um conceito fundamental no projeto e modelagem de bancos de dados relacionais. É uma coluna ou conjunto de colunas em uma tabela que serve para __identificar de forma exclusiva cada registro (linha)__ nessa tabela. A PRIMARY KEY __garante__ a __unicidade__ dos valores nessas colunas e também pode ser usada como referência para estabelecer relacionamentos entre tabelas.

Principais características da PRIMARY KEY:

*   Unicidade: Cada valor na coluna da PRIMARY KEY deve ser único em toda a tabela. Isso significa que não pode haver registros duplicados com o mesmo valor nessa coluna ou conjunto de colunas.

*   Não nulidade: Por padrão, a PRIMARY KEY não permite valores nulos. Cada registro deve ter um valor válido na coluna da chave primária.

*   Rapidez em pesquisas: A PRIMARY KEY é indexada automaticamente, o que permite que o banco de dados encontre rapidamente um registro específico com base nos valores da chave primária. Isso torna as operações de busca eficientes.

### Inserindo dados nas tabelas

Para fazer isso basta apenas executar os seguintes comandos:

```sql
-- Inserindo dados na Tabela departments
INSERT INTO departments (name,) VALUES ('IT');
INSERT INTO departments (name) VALUES ('HR');
INSERT INTO departments (name) VALUES ('Sales');

-- Inserindo dados na Tabela employees
INSERT INTO employees (name, age, department_id) VALUES ('John Doe', 30, 1);
INSERT INTO employees (name, age, department_id) VALUES ('Jane Smith', 28, 2);
INSERT INTO employees (name, age, department_id) VALUES ('Bob Johnson', 35, 1);
INSERT INTO employees (name, age, department_id) VALUES ('Alice Brown', 40, 2);
INSERT INTO employees (name, age, department_id) VALUES ('Mike Davis', 33, 1);
INSERT INTO employees (name, age, department_id) VALUES ('Lisa White', 29, 3);
INSERT INTO employees (name, age, department_id) VALUES ('Tom Green', 42, 3);
INSERT INTO employees (name, age, department_id) VALUES ('Emily Taylor', 27, 2);
INSERT INTO employees (name, age, department_id) VALUES ('David Lee', 31, 1);
INSERT INTO employees (name, age, department_id) VALUES ('Sarah Wilson', 35, 2);

```

### Recuperar dados das tabelas
Para recuperar os dados da tabela departments execute o comando:
```sql
SELECT * FROM departments;
```
Resultado:

| id | name |
|--- |--- |
1|IT|
2|HR|
3|Sales|

Para recuperar os dados da tabela employees execute o comando:
```sql
SELECT * FROM employees;
```
Resultado:

| id | name | age | department_id |
|--- |--- |--- |--- |
1|Sarah Wilson|35|2
2|John Doe|30|1
3|Jane Smith|28|2
4|Bob Johnson|35|1
5|Alice Brown|40|2
6|Mike Davis|33|1
7|Lisa White|29|3
8|Tom Green|42|3
9|Emily Taylor|27|2
10|David Lee|31|1
11|Sarah Wilson|35|2

#### JOIN 

O JOIN é uma cláusula do SQL usada para combinar dados de duas ou mais tabelas com base em colunas relacionadas. Ele permite que você recupere dados relacionados armazenados em tabelas diferentes e os combine em um único conjunto de resultados. Existem diferentes tipos de JOINs que determinam como as tabelas são combinadas. Vamos dar continuidade à nossa conversa anterior e explorar os tipos de JOIN com exemplos usando o SQLite.

##### Tipos de JOIN:

Existem quatro tipos principais de JOIN no SQL: INNER JOIN, LEFT JOIN (ou LEFT OUTER JOIN), RIGHT JOIN (ou RIGHT OUTER JOIN) e FULL JOIN (ou FULL OUTER JOIN). Cada um deles tem um comportamento diferente ao combinar as tabelas.

INNER JOIN:

O INNER JOIN retorna apenas os registros que têm correspondência nas duas tabelas. Ou seja, apenas os registros que têm valores correspondentes na coluna especificada são incluídos no conjunto de resultados.

Exemplo de INNER JOIN:
```sql
SELECT employees.name, departments.name AS department
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;
```
Resultado:

|name| department |
|--- |--- |
Sarah Wilson|HR
John Doe|IT
Jane Smith|HR
Bob Johnson|IT
Alice Brown|HR
Mike Davis|IT
Lisa White|Sales
Tom Green|Sales
Emily Taylor|HR
David Lee|IT
Sarah Wilson|HR

LEFT JOIN (ou LEFT OUTER JOIN):

O LEFT JOIN retorna todos os registros da tabela à esquerda (primeira tabela especificada) e os registros correspondentes da tabela à direita (segunda tabela especificada). Se não houver correspondência na tabela à direita, o resultado conterá NULL nos campos relacionados.

Exemplo de LEFT JOIN:
```sql
SELECT employees.name, departments.name AS department
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;

```

Resultado:

|name| department |
|--- |--- |
Sarah Wilson|HR
John Doe|IT
Jane Smith|HR
Bob Johnson|IT
Alice Brown|HR
Mike Davis|IT
Lisa White|Sales
Tom Green|Sales
Emily Taylor|HR
David Lee|IT
Sarah Wilson|HR

RIGHT JOIN (ou RIGHT OUTER JOIN):

O RIGHT JOIN é semelhante ao LEFT JOIN, mas retorna todos os registros da tabela à direita (segunda tabela especificada) e os registros correspondentes da tabela à esquerda (primeira tabela especificada). Se não houver correspondência na tabela à esquerda, o resultado conterá NULL nos campos relacionados.

Exemplo de RIGHT JOIN:

```sql
SELECT employees.name, departments.name AS department
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.id;
```

Resultado:

|name| department |
|--- |--- |
|Sarah Wilson|	HR|
|John Doe|	IT
|Jane Smith|	HR
|Bob Johnson|	IT
|Alice Brown|	HR
|Mike Davis|	IT
|Lisa White|	Sales
|Tom Green|	Sales
|Emily Taylor|	HR
|David Lee|	IT
|Sarah Wilson|	HR


FULL JOIN (ou FULL OUTER JOIN):

O FULL JOIN retorna todos os registros quando houver uma correspondência em qualquer uma das tabelas. Se não houver correspondência na tabela à esquerda, o resultado conterá NULL nos campos relacionados dessa tabela. Se não houver correspondência na tabela à direita, o resultado conterá NULL nos campos relacionados dessa tabela.

Exemplo de FULL JOIN:

```sql
SELECT employees.name, departments.name AS department
FROM employees
FULL JOIN departments ON employees.department_id = departments.id;
```

Resultado:

|name| department |
|--- |--- |
|Sarah Wilson|	HR
|John Doe|	IT
|Jane Smith|	HR
|Bob Johnson|	IT
|Alice Brown|	HR
|Mike Davis|	IT
|Lisa White|	Sales
|Tom Green|	Sales
|Emily Taylor|	HR
|David Lee|	IT
|Sarah Wilson|	HR

Esses são os principais tipos de JOIN no SQL. Cada um deles é útil em situações diferentes, dependendo de como você deseja combinar os dados entre as tabelas. A escolha do tipo de JOIN adequado depende dos requisitos específicos de consulta e da relação entre as tabelas.

### Consultas com cláusula WHERE, ORDER BY e GROUP BY:

Para filtrar seu resultado use WHERE e para Ordenar seu resultado use ORDER BY:

```sql
SELECT employees.name, departments.name AS department
FROM employees
INNER JOIN departments ON employees.department_id = departments.id
WHERE departments.name = "IT" ORDER BY employees.name DESC;
```

Resultado:

|name| department |
|--- |--- |
|Mike Davis|	IT
|John Doe|	IT
|David Lee|	IT
|Bob Johnson|	IT


### Em construção...