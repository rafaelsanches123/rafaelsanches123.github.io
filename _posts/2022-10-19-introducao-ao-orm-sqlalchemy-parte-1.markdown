---
layout: post
title: "Introdução a manipulação de banco de dados com a biblioteca ORM Sqlalchemy - Parte 1"
date: 2022-10-19 17:00:03 -0300
categories: python sql orm sqlalchemy
---

![database-schema]({{ site.url }}/assets/database-schema.png){:style="width: 100%" }

Fala pessoal blz? No post de hoje vamos trocar uma ideia sobre a biblioteca ORM __SQLALCHEMY__ utilizada com python para manipulação de bancos de dados. E aí, bora aprender algo novo?

## INTRODUÇÃO AO FRAMEWORK SQL ALCHEMY

__SQL ALCHEMY__ é um __framework__ do tipo __Mapeamento objeto-relacional__ ou simplesmente __ORM__. Isso significa que por meio da linguagem python e orientação a objetos é possível converter código python e entidades de dados e também realizar o gerenciamento das mesmas. A seguir, vou ilustrar como isso funciona passo a passo para te ajudar a se tornar um profissional melhor.

## INSTALANDO A BIBLIOTECA DO SQL ALCHEMY NO PYTHON 3


```python
# no seu terminal digite apenas => pip install SQLAlchemy
# o comando abaixo com ! é por eu estar executando em um notebook que estou preparando esse tutorial
#!pip install SQLAlchemy
from sqlalchemy.exc import SQLAlchemyError #USAMOS ESSE OBJETO DA BIBLIOTECA SQLACHEMY PARA RECUPERAR OS ERROS QUE PODEM OCORRER DURANTE AS INTERAÇÕES COM O BANCO DE DADOS
from sqlalchemy import inspect #USAMOS ESSE OBJETO DA BIBLIOTECA SQLACHEMY PARA VERIFICAR SE ALGUMA TABELA NOSSA QUE DESEJAMOS CRIAR JÁ POSSA EXISTIR E PODERMOS TOMAR ALGUMA DECISÃO QUANTO A ISSO
```

## CRIANDO UMA ENGINE

O engine é como o SQLAlchemy se comunica com o banco de dados. Portanto, ao criar o mecanismo, você deve adicionar a URL do banco de dados e é basicamente isso. A seguir vou utilizar o sqlite por sem bem simples e fácil de outras pessoas conseguirem reproduzir esse tutotial, mas se você quiser basta pesquisar na internet o modo de se comunicar com o banco de dados que você utiliza seja ele Mysql, SqlServer, Oracle etc... 


```python
from sqlalchemy import create_engine
# Para utilizar o debug deve-se adicionar ``echo=True``: ele permite que ao interagir com o banco você visualize todos os comandos executados pelo SQLAlchemy
database_url = 'sqlite:///teste.db'
engine = create_engine(database_url, echo=True)
engine
```




    Engine(sqlite:///teste.db)


![engine-sqlalchemy]({{ site.url }}/assets/engine_sqlalchemy.png){:style="width: 100%" }

Com a engine pronta você pode se conectar e manipular um banco de dados de 2 formas possíveis. A seguir eu apresento a primeira forma que permite a manipulação de uma banco de dados forma direta:


```python
# EXEMPLO DE CONSULTA DE DATA ATUAL USANDO SQL
conn = engine.connect()
trans = conn.begin()
query = 'SELECT DATE();'
result = conn.execute(query)
for row in result:
    print(f"DATE = {row[0]}")
trans.commit()
conn.close()
```

    2022-12-03 12:50:17,663 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:17,664 INFO sqlalchemy.engine.Engine SELECT DATE();
    2022-12-03 12:50:17,665 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">DATE = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>-<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">12</span>-<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">03</span>
</pre>



    2022-12-03 12:50:17,669 INFO sqlalchemy.engine.Engine COMMIT


## LEMBRETE

Nunca se esqueça que se você abrir uma conexão, você precisa fecha-lá ao terminar de manipular os dados no banco de dados. Também é importante fechar qualquer transação que você abra após terminar de manipular os dados. A conexão permite que você converse com o banco de dados. A transação garante que o banco execute o comando que você deseja que ele realize.

```python
conn = engine.connect() #ABRIR CONEXÃO COM O BANCO DE DADOS
trans = conn.begin() #ABRIR TRANSAÇÃO PARA MANIPULAR OS DADOS

# aqui nesse espaço você constroe suas consultas ou outro tipo de ação que desejar realizar

trans.commit() #FECHAR A TRANSAÇÃO ABERTA ANTERIORMENTE PARA MANIPULAR OS DADOS
conn.close() #FECHAR A CONEXÃO COM O BANCO DE DADOS
```

## CRIANDO UMA FUNÇÃO QUE RETORNA SE UMA TABELA JÁ EXISTE OU NÃO


```python
inspector = inspect(engine)
def tabela_ja_existe(nome_tabela):
    print(f"VALIDANDO SE A TABELA {nome_tabela} JÁ EXISTE OU NÃO")
    if nome_tabela in inspector.get_table_names():
        return True
    else:
        return False
```

## CRIANDO TABELAS

Se as tabelas já existirem você irá receber um erro ao executar o bloco a baixo. Caso as tabelas ainda não existam elas serão criadas.


```python
#AQUI TEMOS AS TABELAS QUE DESEJAMOS CRIAR
tabelas = ["funcionarios", "departamentos", "trabalha"]

#EXIBINDO OS NOMES DE NOSSAS TABELAS QUE INFORMAMOS NA LISTA ACIMA
print("EXIBINDO OS NOMES DE NOSSAS TABELAS QUE DESEJAMOS CRIAR:")
print("TABELA: ", tabelas[0])
print("TABELA: ", tabelas[1])
print("TABELA: ", tabelas[2])
print("\n\n\n")

ddl_1 = """
CREATE TABLE IF NOT EXISTS {} (
    id INTEGER PRIMARY KEY,
    nome TEXT,
    idade INT,
    salario DECIMAL(10,3)
);
""".format(tabelas[0])

ddl_2 = """
CREATE TABLE IF NOT EXISTS {} (
    id INTEGER PRIMARY KEY,
    nome TEXT
);
""".format(tabelas[1])

ddl_3 = """
CREATE TABLE IF NOT EXISTS {} (
    id INTEGER PRIMARY KEY,
    id_funcionario INT,
    id_departamento INT,
    data_entrada DATE,
    data_saida DATE,
    FOREIGN KEY (id_funcionario) REFERENCES funcionarios (id),
    FOREIGN KEY (id_departamento) REFERENCES departamentos (id)
);
""".format(tabelas[2])

conn = engine.connect()
trans = conn.begin()

if tabela_ja_existe(tabelas[0]) == False:
    try:
        conn.execute(ddl_1)
    except Exception as e:
        print(e,"\n\n\n")
        console.print_exception(show_locals=True)
else:
    print(f"Tabela {tabelas[0]} já existe!")
#==============================================
if tabela_ja_existe(tabelas[1]) == False:
    try:
        conn.execute(ddl_2)
    except Exception as e:
        print(e,"\n\n\n")
        console.print_exception(show_locals=True)
else:
    print(f"Tabela {tabelas[1]} já existe!")
#==============================================
if tabela_ja_existe(tabelas[2]) == False:
    try:
        conn.execute(ddl_3)
    except Exception as e:
        print(e,"\n\n\n")
        console.print_exception(show_locals=True)
else:
    print(f"Tabela {tabelas[2]} já existe!")


trans.commit()
conn.close()
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">EXIBINDO OS NOMES DE NOSSAS TABELAS QUE DESEJAMOS CRIAR:
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">TABELA:  funcionarios
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">TABELA:  departamentos
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">TABELA:  trabalha
</pre>


    2022-12-03 12:50:17,766 INFO sqlalchemy.engine.Engine BEGIN (implicit)



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">VALIDANDO SE A TABELA funcionarios JÁ EXISTE OU NÃO
</pre>



    2022-12-03 12:50:17,769 INFO sqlalchemy.engine.Engine SELECT name FROM sqlite_master WHERE type='table' ORDER BY name
    2022-12-03 12:50:17,770 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:17,771 INFO sqlalchemy.engine.Engine 
    CREATE TABLE IF NOT EXISTS funcionarios (
        id INTEGER PRIMARY KEY,
        nome TEXT,
        idade INT,
        salario DECIMAL(10,3)
    );
    
    2022-12-03 12:50:17,772 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">VALIDANDO SE A TABELA departamentos JÁ EXISTE OU NÃO
</pre>



    2022-12-03 12:50:17,867 INFO sqlalchemy.engine.Engine 
    CREATE TABLE IF NOT EXISTS departamentos (
        id INTEGER PRIMARY KEY,
        nome TEXT
    );
    
    2022-12-03 12:50:17,868 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">VALIDANDO SE A TABELA trabalha JÁ EXISTE OU NÃO
</pre>



    2022-12-03 12:50:17,923 INFO sqlalchemy.engine.Engine 
    CREATE TABLE IF NOT EXISTS trabalha (
        id INTEGER PRIMARY KEY,
        id_funcionario INT,
        id_departamento INT,
        data_entrada DATE,
        data_saida DATE,
        FOREIGN KEY (id_funcionario) REFERENCES funcionarios (id),
        FOREIGN KEY (id_departamento) REFERENCES departamentos (id)
    );
    
    2022-12-03 12:50:17,925 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:17,976 INFO sqlalchemy.engine.Engine COMMIT


## INSERINDO DADOS NAS TABELAS


```python
# PARTINDO DO PENSAMENTO DE QUE JÁ TEMOS AS TABELAS CRIADAS COM SUCESSO, AGORA DESEJAMOS INSERIR INFORMAÇÕES NAS TABELAS
conn = engine.connect()
trans = conn.begin()
try:
    comando_sql = """
    INSERT INTO {} (nome, idade, salario) 
    VALUES ('Hephzibah', 38, 306.261),
    ('Paxon', 65, 428.725),
    ('Corty', 48, 198.27),
    ('Hedy', 46, 440.927),
    ('Elyse', 39, 480.426),
    ('Ira', 21, 186.163),
    ('Mattias', 43, 344.029),
    ('Tybalt', 57, 363.227),
    ('Sully', 40, 282.221),
    ('Wrennie', 41, 122.309),
    ('Anatol', 60, 176.018),
    ('Craggie', 69, 201.606),
    ('Aila', 20, 358.59),
    ('Marylin', 40, 163.559),
    ('Moselle', 48, 306.284),
    ('Raleigh', 23, 430.375),
    ('Tracey', 31, 109.874),
    ('Olenolin', 40, 190.977),
    ('Myranda', 49, 324.872),
    ('Filberto', 24, 362.89),
    ('Calvin', 37, 498.879); 
     """.format(tabelas[0])
    conn.execute(comando_sql)
except SQLAlchemyError as e:
    print(e,"\n\n\n")
try:
    comando_sql = """
    INSERT INTO {} (nome) 
    VALUES ('Human Resources'),
    ('Services'),
    ('Product Management'),
    ('Support'),
    ('Business Development'),
    ('Services'),
    ('Human Resources'),
    ('Support'),
    ('Engineering'),
    ('Services');
    """.format(tabelas[1])
    conn.execute(comando_sql)
except SQLAlchemyError as e:
    print(e,"\n\n\n")
    console.print_exception(show_locals=True)
try:
    comando_sql = """
    INSERT INTO {} (id_funcionario, id_departamento, data_entrada, data_saida) 
    VALUES (1, 4, '7/8/2022', '10/8/2021'),
    (2, 5, '1/10/2022', '3/14/2022'),
    (3, 7, '3/3/2021', '6/24/2021'),
    (4, 10, '1/4/2022', '11/27/2021'),
    (5, 3, '5/20/2022', '2/20/2021'),
    (6, 5, '9/7/2021', '10/11/2022'),
    (7, 6, '5/29/2021', '7/11/2022'),
    (8, 5, '2/18/2022', '5/28/2022'),
    (9, 3, '3/17/2022', null),
    (10, 9, '1/31/2022', '10/11/2021'),
    (11, 9, '2/6/2022', null),
    (12, 2, '9/28/2021', null),
    (13, 6, '2/28/2021', '4/6/2022'),
    (14, 5, '11/25/2022', null),
    (15, 10, '8/8/2021', '6/16/2021'),
    (16, 5, '8/1/2022', null),
    (17, 1, '5/26/2022', null),
    (18, 6, '11/13/2021', null),
    (19, 8, '6/22/2022', '12/11/2022'),
    (20, 5, '2/19/2021', '7/11/2022'),
    (21, 1, '9/7/2021', null);
    """.format(tabelas[2])
    conn.execute(comando_sql)
except SQLAlchemyError as e:
    print(e,"\n\n\n")
    console.print_exception(show_locals=True)
trans.commit()
conn.close()
```

    2022-12-03 12:50:17,985 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:17,987 INFO sqlalchemy.engine.Engine 
        INSERT INTO funcionarios (nome, idade, salario) 
        VALUES ('Hephzibah', 38, 306.261),
        ('Paxon', 65, 428.725),
        ('Corty', 48, 198.27),
        ('Hedy', 46, 440.927),
        ('Elyse', 39, 480.426),
        ('Ira', 21, 186.163),
        ('Mattias', 43, 344.029),
        ('Tybalt', 57, 363.227),
        ('Sully', 40, 282.221),
        ('Wrennie', 41, 122.309),
        ('Anatol', 60, 176.018),
        ('Craggie', 69, 201.606),
        ('Aila', 20, 358.59),
        ('Marylin', 40, 163.559),
        ('Moselle', 48, 306.284),
        ('Raleigh', 23, 430.375),
        ('Tracey', 31, 109.874),
        ('Olenolin', 40, 190.977),
        ('Myranda', 49, 324.872),
        ('Filberto', 24, 362.89),
        ('Calvin', 37, 498.879); 
         
    2022-12-03 12:50:17,988 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:17,990 INFO sqlalchemy.engine.Engine 
        INSERT INTO departamentos (nome) 
        VALUES ('Human Resources'),
        ('Services'),
        ('Product Management'),
        ('Support'),
        ('Business Development'),
        ('Services'),
        ('Human Resources'),
        ('Support'),
        ('Engineering'),
        ('Services');
        
    2022-12-03 12:50:17,991 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:17,992 INFO sqlalchemy.engine.Engine 
        INSERT INTO trabalha (id_funcionario, id_departamento, data_entrada, data_saida) 
        VALUES (1, 4, '7/8/2022', '10/8/2021'),
        (2, 5, '1/10/2022', '3/14/2022'),
        (3, 7, '3/3/2021', '6/24/2021'),
        (4, 10, '1/4/2022', '11/27/2021'),
        (5, 3, '5/20/2022', '2/20/2021'),
        (6, 5, '9/7/2021', '10/11/2022'),
        (7, 6, '5/29/2021', '7/11/2022'),
        (8, 5, '2/18/2022', '5/28/2022'),
        (9, 3, '3/17/2022', null),
        (10, 9, '1/31/2022', '10/11/2021'),
        (11, 9, '2/6/2022', null),
        (12, 2, '9/28/2021', null),
        (13, 6, '2/28/2021', '4/6/2022'),
        (14, 5, '11/25/2022', null),
        (15, 10, '8/8/2021', '6/16/2021'),
        (16, 5, '8/1/2022', null),
        (17, 1, '5/26/2022', null),
        (18, 6, '11/13/2021', null),
        (19, 8, '6/22/2022', '12/11/2022'),
        (20, 5, '2/19/2021', '7/11/2022'),
        (21, 1, '9/7/2021', null);
        
    2022-12-03 12:50:17,993 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:17,995 INFO sqlalchemy.engine.Engine COMMIT


## RECUPERANDO OS DADOS DAS TABELAS


```python
conn = engine.connect() #ABRIR CONEXÃO COM O BANCO DE DADOS
trans = conn.begin() #ABRIR TRANSAÇÃO PARA MANIPULAR OS DADOS

print("######################## RECUPERANDO OS DADOS DOS FUNCIONARIOS ########################")

comando_sql = """
SELECT * FROM funcionarios;
"""
funcionarios = conn.execute(comando_sql)

for f in funcionarios:
    print(f)

print("######################## RECUPERANDO OS DADOS DOS DEPARTAMENTOS ########################")

comando_sql = """
SELECT * FROM departamentos;
"""
departamentos = conn.execute(comando_sql)

for d in departamentos:
    print(d)

print("######################## RECUPERANDO OS DADOS DOS FUNCIONARIOS QUEM TRABALHAM NOS DEPARTAMENTOS ########################")

comando_sql = """
SELECT f.nome, f.idade, f.salario, d.nome, t.data_entrada, t.data_saida FROM trabalha as t JOIN funcionarios as f ON t.id_funcionario = f.id JOIN departamentos d ON t.id_departamento = d.id;
"""
trabalham = conn.execute(comando_sql)

for t in trabalham:
    print(t)

trans.commit() #FECHAR A TRANSAÇÃO ABERTA ANTERIORMENTE PARA MANIPULAR OS DADOS
conn.close() #FECHAR A CONEXÃO COM O BANCO DE DADOS
```

    2022-12-03 12:50:18,098 INFO sqlalchemy.engine.Engine BEGIN (implicit)



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">######################## RECUPERANDO OS DADOS DOS FUNCIONARIOS ########################
</pre>



    2022-12-03 12:50:18,103 INFO sqlalchemy.engine.Engine 
    SELECT * FROM funcionarios;
    
    2022-12-03 12:50:18,104 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #008000; text-decoration-color: #008000">'Hephzibah'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">38</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.261</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #008000; text-decoration-color: #008000">'Paxon'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">65</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">428.725</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #008000; text-decoration-color: #008000">'Corty'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">198.27</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #008000; text-decoration-color: #008000">'Hedy'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">46</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">440.927</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #008000; text-decoration-color: #008000">'Elyse'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">39</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">480.426</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #008000; text-decoration-color: #008000">'Ira'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">186.163</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #008000; text-decoration-color: #008000">'Mattias'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">43</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">344.029</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #008000; text-decoration-color: #008000">'Tybalt'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">57</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">363.227</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #008000; text-decoration-color: #008000">'Sully'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">282.221</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #008000; text-decoration-color: #008000">'Wrennie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">41</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">122.309</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>, <span style="color: #008000; text-decoration-color: #008000">'Anatol'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">60</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">176.018</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">12</span>, <span style="color: #008000; text-decoration-color: #008000">'Craggie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">69</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">201.606</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">13</span>, <span style="color: #008000; text-decoration-color: #008000">'Aila'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">358.59</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">14</span>, <span style="color: #008000; text-decoration-color: #008000">'Marylin'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">163.559</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">15</span>, <span style="color: #008000; text-decoration-color: #008000">'Moselle'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.284</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">16</span>, <span style="color: #008000; text-decoration-color: #008000">'Raleigh'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">23</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">430.375</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">17</span>, <span style="color: #008000; text-decoration-color: #008000">'Tracey'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">31</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">109.874</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">18</span>, <span style="color: #008000; text-decoration-color: #008000">'Olenolin'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">190.977</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">19</span>, <span style="color: #008000; text-decoration-color: #008000">'Myranda'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">49</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">324.872</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #008000; text-decoration-color: #008000">'Filberto'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">24</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">362.89</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #008000; text-decoration-color: #008000">'Calvin'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">37</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">498.879</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">######################## RECUPERANDO OS DADOS DOS DEPARTAMENTOS ########################
</pre>



    2022-12-03 12:50:18,144 INFO sqlalchemy.engine.Engine 
    SELECT * FROM departamentos;
    
    2022-12-03 12:50:18,145 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #008000; text-decoration-color: #008000">'Human Resources'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #008000; text-decoration-color: #008000">'Product Management'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #008000; text-decoration-color: #008000">'Support'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #008000; text-decoration-color: #008000">'Human Resources'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #008000; text-decoration-color: #008000">'Support'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #008000; text-decoration-color: #008000">'Engineering'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">######################## RECUPERANDO OS DADOS DOS FUNCIONARIOS QUEM TRABALHAM NOS DEPARTAMENTOS 
########################
</pre>



    2022-12-03 12:50:18,159 INFO sqlalchemy.engine.Engine 
    SELECT f.nome, f.idade, f.salario, d.nome, t.data_entrada, t.data_saida FROM trabalha as t JOIN funcionarios as f ON t.id_funcionario = f.id JOIN departamentos d ON t.id_departamento = d.id;
    
    2022-12-03 12:50:18,159 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Hephzibah'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">38</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.261</span>, <span style="color: #008000; text-decoration-color: #008000">'Support'</span>, <span style="color: #008000; text-decoration-color: #008000">'7/8/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'10/8/2021'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Paxon'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">65</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">428.725</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span>, <span style="color: #008000; text-decoration-color: #008000">'1/10/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'3/14/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Corty'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">198.27</span>, <span style="color: #008000; text-decoration-color: #008000">'Human Resources'</span>, <span style="color: #008000; text-decoration-color: #008000">'3/3/2021'</span>, <span style="color: #008000; text-decoration-color: #008000">'6/24/2021'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Hedy'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">46</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">440.927</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span>, <span style="color: #008000; text-decoration-color: #008000">'1/4/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'11/27/2021'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Elyse'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">39</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">480.426</span>, <span style="color: #008000; text-decoration-color: #008000">'Product Management'</span>, <span style="color: #008000; text-decoration-color: #008000">'5/20/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'2/20/2021'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Ira'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">186.163</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span>, <span style="color: #008000; text-decoration-color: #008000">'9/7/2021'</span>, <span style="color: #008000; text-decoration-color: #008000">'10/11/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Mattias'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">43</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">344.029</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span>, <span style="color: #008000; text-decoration-color: #008000">'5/29/2021'</span>, <span style="color: #008000; text-decoration-color: #008000">'7/11/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Tybalt'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">57</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">363.227</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span>, <span style="color: #008000; text-decoration-color: #008000">'2/18/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'5/28/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Sully'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">282.221</span>, <span style="color: #008000; text-decoration-color: #008000">'Product Management'</span>, <span style="color: #008000; text-decoration-color: #008000">'3/17/2022'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Wrennie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">41</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">122.309</span>, <span style="color: #008000; text-decoration-color: #008000">'Engineering'</span>, <span style="color: #008000; text-decoration-color: #008000">'1/31/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'10/11/2021'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Anatol'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">60</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">176.018</span>, <span style="color: #008000; text-decoration-color: #008000">'Engineering'</span>, <span style="color: #008000; text-decoration-color: #008000">'2/6/2022'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Craggie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">69</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">201.606</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span>, <span style="color: #008000; text-decoration-color: #008000">'9/28/2021'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Aila'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">358.59</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span>, <span style="color: #008000; text-decoration-color: #008000">'2/28/2021'</span>, <span style="color: #008000; text-decoration-color: #008000">'4/6/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Marylin'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">163.559</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span>, <span style="color: #008000; text-decoration-color: #008000">'11/25/2022'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Moselle'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.284</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span>, <span style="color: #008000; text-decoration-color: #008000">'8/8/2021'</span>, <span style="color: #008000; text-decoration-color: #008000">'6/16/2021'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Raleigh'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">23</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">430.375</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span>, <span style="color: #008000; text-decoration-color: #008000">'8/1/2022'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Tracey'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">31</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">109.874</span>, <span style="color: #008000; text-decoration-color: #008000">'Human Resources'</span>, <span style="color: #008000; text-decoration-color: #008000">'5/26/2022'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Olenolin'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">190.977</span>, <span style="color: #008000; text-decoration-color: #008000">'Services'</span>, <span style="color: #008000; text-decoration-color: #008000">'11/13/2021'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Myranda'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">49</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">324.872</span>, <span style="color: #008000; text-decoration-color: #008000">'Support'</span>, <span style="color: #008000; text-decoration-color: #008000">'6/22/2022'</span>, <span style="color: #008000; text-decoration-color: #008000">'12/11/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Filberto'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">24</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">362.89</span>, <span style="color: #008000; text-decoration-color: #008000">'Business Development'</span>, <span style="color: #008000; text-decoration-color: #008000">'2/19/2021'</span>, <span style="color: #008000; text-decoration-color: #008000">'7/11/2022'</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008000; text-decoration-color: #008000">'Calvin'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">37</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">498.879</span>, <span style="color: #008000; text-decoration-color: #008000">'Human Resources'</span>, <span style="color: #008000; text-decoration-color: #008000">'9/7/2021'</span>, <span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>



    2022-12-03 12:50:18,209 INFO sqlalchemy.engine.Engine COMMIT


## ATUALIZANDO OS DADOS NAS TABELAS

Para esse exemplo vamos selecionar os 10 primeiros funcionários e escolher um deles para realizar alguma alteração como por exemplo o valor do salário.


```python
conn = engine.connect()
trans = conn.begin()
query = 'SELECT * FROM funcionarios LIMIT 10;' #CONSULTA PARA SELECIONAR OS 10 PRIMEIROS FUNCIONÁRIOS CADASTRADOS NO NOSSO BANCO DE DADOS
result = conn.execute(query)
for row in result:
    print(row)
trans.commit()
conn.close()
```

    2022-12-03 12:50:18,216 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:18,217 INFO sqlalchemy.engine.Engine SELECT * FROM funcionarios LIMIT 10;
    2022-12-03 12:50:18,218 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #008000; text-decoration-color: #008000">'Hephzibah'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">38</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.261</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #008000; text-decoration-color: #008000">'Paxon'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">65</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">428.725</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #008000; text-decoration-color: #008000">'Corty'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">198.27</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #008000; text-decoration-color: #008000">'Hedy'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">46</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">440.927</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #008000; text-decoration-color: #008000">'Elyse'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">39</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">480.426</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #008000; text-decoration-color: #008000">'Ira'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">186.163</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #008000; text-decoration-color: #008000">'Mattias'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">43</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">344.029</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #008000; text-decoration-color: #008000">'Tybalt'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">57</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">363.227</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #008000; text-decoration-color: #008000">'Sully'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">282.221</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #008000; text-decoration-color: #008000">'Wrennie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">41</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">122.309</span><span style="font-weight: bold">)</span>
</pre>



    2022-12-03 12:50:18,242 INFO sqlalchemy.engine.Engine COMMIT



```python
conn = engine.connect()
trans = conn.begin()
try:
    comando_sql = """
    UPDATE funcionarios
    SET nome = 'Rafael', salario = 50000.00
    WHERE id = 3;
    """
    conn.execute(comando_sql)
except SQLAlchemyError as e:
    print(e,"\n\n\n")
    console.print_exception(show_locals=True)
trans.commit()
conn.close()
```

    2022-12-03 12:50:18,258 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:18,259 INFO sqlalchemy.engine.Engine 
        UPDATE funcionarios
        SET nome = 'Rafael', salario = 50000.00
        WHERE id = 3;
        
    2022-12-03 12:50:18,260 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:18,263 INFO sqlalchemy.engine.Engine COMMIT



```python
conn = engine.connect()
trans = conn.begin()
query = 'SELECT * FROM funcionarios LIMIT 10;' #CONSULTA PARA SELECIONAR OS 10 PRIMEIROS FUNCIONÁRIOS CADASTRADOS NO NOSSO BANCO DE DADOS
result = conn.execute(query)
for row in result:
    print(row)
trans.commit()
conn.close()
```

    2022-12-03 12:50:18,363 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:18,364 INFO sqlalchemy.engine.Engine SELECT * FROM funcionarios LIMIT 10;
    2022-12-03 12:50:18,364 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #008000; text-decoration-color: #008000">'Hephzibah'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">38</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.261</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #008000; text-decoration-color: #008000">'Paxon'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">65</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">428.725</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #008000; text-decoration-color: #008000">'Rafael'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">50000</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #008000; text-decoration-color: #008000">'Hedy'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">46</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">440.927</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #008000; text-decoration-color: #008000">'Elyse'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">39</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">480.426</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #008000; text-decoration-color: #008000">'Ira'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">186.163</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #008000; text-decoration-color: #008000">'Mattias'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">43</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">344.029</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #008000; text-decoration-color: #008000">'Tybalt'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">57</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">363.227</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #008000; text-decoration-color: #008000">'Sully'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">282.221</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #008000; text-decoration-color: #008000">'Wrennie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">41</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">122.309</span><span style="font-weight: bold">)</span>
</pre>



    2022-12-03 12:50:18,378 INFO sqlalchemy.engine.Engine COMMIT


## DELETANDOS OS DADOS NAS TABELAS


```python
# VAMOS DELETAR O REGISTRO COM ID = 4 referente a => (4, 'Hedy', 46, 440.927)
conn = engine.connect()
trans = conn.begin()
try:
    comando_sql = """
    DELETE FROM funcionarios WHERE id = 4; 
    """
    conn.execute(comando_sql)
except SQLAlchemyError as e:
    print(e,"\n\n\n")
    console.print_exception(show_locals=True)
trans.commit()
conn.close()
```

    2022-12-03 12:50:18,427 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:18,428 INFO sqlalchemy.engine.Engine 
        DELETE FROM funcionarios WHERE id = 4; 
        
    2022-12-03 12:50:18,429 INFO sqlalchemy.engine.Engine [raw sql] ()
    2022-12-03 12:50:18,431 INFO sqlalchemy.engine.Engine COMMIT



```python
conn = engine.connect()
trans = conn.begin()
query = 'SELECT * FROM funcionarios LIMIT 10;' #CONSULTA PARA SELECIONAR OS 10 PRIMEIROS FUNCIONÁRIOS CADASTRADOS NO NOSSO BANCO DE DADOS
result = conn.execute(query)
for row in result:
    print(row)
trans.commit()
conn.close()
```

    2022-12-03 12:50:18,526 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2022-12-03 12:50:18,527 INFO sqlalchemy.engine.Engine SELECT * FROM funcionarios LIMIT 10;
    2022-12-03 12:50:18,528 INFO sqlalchemy.engine.Engine [raw sql] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #008000; text-decoration-color: #008000">'Hephzibah'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">38</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.261</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #008000; text-decoration-color: #008000">'Paxon'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">65</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">428.725</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #008000; text-decoration-color: #008000">'Rafael'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">50000</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #008000; text-decoration-color: #008000">'Elyse'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">39</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">480.426</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #008000; text-decoration-color: #008000">'Ira'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">186.163</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #008000; text-decoration-color: #008000">'Mattias'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">43</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">344.029</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #008000; text-decoration-color: #008000">'Tybalt'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">57</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">363.227</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #008000; text-decoration-color: #008000">'Sully'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">282.221</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #008000; text-decoration-color: #008000">'Wrennie'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">41</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">122.309</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>, <span style="color: #008000; text-decoration-color: #008000">'Anatol'</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">60</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">176.018</span><span style="font-weight: bold">)</span>
</pre>



    2022-12-03 12:50:18,545 INFO sqlalchemy.engine.Engine COMMIT


Como foi possível representar nos 2 últimos trechos de código nos escolhemos um registro da tabela funcionários que nesse caso foi o usuário que tinha o id = 4. Logo depois de realizar a exclusão desse registro nos realizamos um comando SELECT para trazer os 10 primeiros registros e já é possível visualizar que o número 4 não pertence mais a tabela. Nesse post eu mostrei de forma simples e direta como manipular uma base de dados usando linguagem PYTHON com SQL para manipular o banco de dados SQLITE3 que é um banco bastante simples geralmente usado para realização de provas de conceito (POCs) e também em ambientes de desenvolvimento para validar ideias.

No próximo post eu vou ensinar como utilizar os recursos mais utilizados do ORM SQLACHEMY para realizar as mesmas atividades que foram demostradas nesse post para que você que está lendo esse post possa tirar ainda mais proveito da manipulação de bancos de dados com python.