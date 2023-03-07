---
layout: post
title: "Introdução a manipulação de banco de dados com a biblioteca ORM Sqlalchemy - Parte 2"
date: 2023-03-06 17:00:03 -0300
categories: python sql orm sqlalchemy
---

![database-schema]({{ site.url }}/assets/database-schema.png){:style="width: 100%" }

Fala pessoal blz? No post de hoje vamos trocar uma ideia sobre a biblioteca ORM __SQLALCHEMY__ utilizada com python para manipulação de bancos de dados. E aí, bora aprender algo novo?

Se você ainda não viu [POST de INTRODUÇÃO AO SQLALCHEMY](https://tudoprogramado.blog.br/introducao-ao-orm-sqlalchemy-parte-1) recomendo começar seus estudos por ele caso ainda não tenha nenhum contato com esse framework incrivel. Caso, você só queira ver a parte relacionado ao uso desse framework mais voltado a manipulação de dados usando Orientação a Objetos então, te recomendo a continuar a leitura a seguir...


# EM CONSTRUÇÃO... NÃO CONSIDERAR TUDO A SEGUIR POIS ESTÁ SENDO ATUALIZADO...


```python
from rich import print #Biblioteca utilizada para dar mais vida ao terminal do computador
from rich.console import Console # faz parte da biblioteca acima
console = Console()
from sqlalchemy.exc import SQLAlchemyError #USAMOS ESSE OBJETO DA BIBLIOTECA SQLACHEMY PARA RECUPERAR OS ERROS QUE PODEM OCORRER DURANTE AS INTERAÇÕES COM O BANCO DE DADOS
from sqlalchemy import inspect #USAMOS ESSE OBJETO DA BIBLIOTECA SQLACHEMY PARA VERIFICAR SE ALGUMA TABELA NOSSA QUE DESEJAMOS CRIAR JÁ POSSA EXISTIR E PODERMOS TOMAR ALGUMA DECISÃO QUANTO A ISSO
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
import datetime
```


```python
database_url = 'sqlite:///teste.db'
engine = create_engine(database_url, echo=True)
engine
```




    Engine(sqlite:///teste.db)




```python
from sqlalchemy import Column, Integer, String, Float, Date, ForeignKey
from sqlalchemy.orm import declarative_base
from sqlalchemy.orm import relationship

# declarative base class
Base = declarative_base()

# an example mapping using the base
class Funcionario(Base):
    __tablename__ = "funcionarios"

    id = Column(Integer, primary_key=True)
    nome = Column(String)
    idade = Column(Integer)
    salario = Column(Float)
    
    def __repr__(self): # show collumn values in some object that represent a table from database
        return f"Funcionario(id={self.id}, nome={self.nome}, idade={self.idade}, salario={self.salario})"

class Departamento(Base):
    __tablename__ = "departamentos"
    id = Column(Integer, primary_key=True)
    nome = Column(String)
    
    def __repr__(self):
        return f"Departamento(id={self.id}, nome={self.nome})"
    

class Trabalha(Base):
    __tablename__ = "trabalha"
    id = Column(Integer, primary_key=True)
    id_funcionario = Column(Integer, ForeignKey("funcionarios.id"))
    id_departamento = Column(Integer, ForeignKey("departamentos.id"))
    data_entrada = Column(String)
    data_saida = Column(String)
    
    def __repr__(self):
        return f"Funcionario(id={self.id}, id_funcionario={self.id_funcionario}, id_departamento={self.id_departamento}, data_entrada={self.data_entrada}, data_saida={self.data_saida})"
    
#Base.metadata.create_all(engine)
```


```python
from sqlalchemy import select
# Criando uma sessão (add, commit, query, etc).
Session = sessionmaker(engine)
# verbose version of what a context manager will do
with Session() as session:
    session.begin()
    try:
        funcionarios = session.scalars(select(Funcionario)).all()
        for f in funcionarios:
            print(f)
    except:
        session.rollback()
        raise
    else:
        session.commit()
```

    2023-02-07 21:56:53,947 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2023-02-07 21:56:53,952 INFO sqlalchemy.engine.Engine SELECT funcionarios.id, funcionarios.nome, funcionarios.idade, funcionarios.salario 
    FROM funcionarios
    2023-02-07 21:56:53,954 INFO sqlalchemy.engine.Engine [generated in 0.00179s] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Hephzibah</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">38</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.261</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Paxon</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">65</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">428.725</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Rafael</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">50000</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Elyse</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">39</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">480.426</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Ira</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">186.163</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Mattias</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">43</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">344.029</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Tybalt</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">57</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">363.227</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Sully</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">282.221</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Wrennie</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">41</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">122.309</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Anatol</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">60</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">176.018</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">12</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Craggie</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">69</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">201.606</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">13</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Aila</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">358.59</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">14</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Marylin</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">163.559</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">15</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Moselle</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">48</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">306.284</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">16</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Raleigh</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">23</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">430.375</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">17</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Tracey</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">31</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">109.874</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">18</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Olenolin</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">40</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">190.977</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">19</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Myranda</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">49</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">324.872</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Filberto</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">24</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">362.89</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Calvin</span>, <span style="color: #808000; text-decoration-color: #808000">idade</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">37</span>, <span style="color: #808000; text-decoration-color: #808000">salario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">498.879</span><span style="font-weight: bold">)</span>
</pre>



    2023-02-07 21:56:53,996 INFO sqlalchemy.engine.Engine COMMIT



```python
from sqlalchemy import select
# Criando uma sessão (add, commit, query, etc).
Session = sessionmaker(engine)
# verbose version of what a context manager will do
with Session() as session:
    session.begin()
    try:
        departamentos = session.scalars(select(Departamento)).all()
        for d in departamentos:
            print(d)
    except:
        session.rollback()
        raise
    else:
        session.commit()
```

    2023-02-07 21:56:54,020 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2023-02-07 21:56:54,023 INFO sqlalchemy.engine.Engine SELECT departamentos.id, departamentos.nome 
    FROM departamentos
    2023-02-07 21:56:54,024 INFO sqlalchemy.engine.Engine [generated in 0.00162s] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Human</span> Resources<span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Services</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Product</span> Management<span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Support</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Business</span> Development<span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Services</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Human</span> Resources<span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Support</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Engineering</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Departamento</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #808000; text-decoration-color: #808000">nome</span>=<span style="color: #800080; text-decoration-color: #800080">Services</span><span style="font-weight: bold">)</span>
</pre>



    2023-02-07 21:56:54,045 INFO sqlalchemy.engine.Engine COMMIT



```python
from sqlalchemy import select
# Criando uma sessão (add, commit, query, etc).
Session = sessionmaker(engine)
# verbose version of what a context manager will do
with Session() as session:
    session.begin()
    try:
        
        trabalha = session.scalars(select(Trabalha)).all()
        for t in trabalha:
            print(t)
    except:
        session.rollback()
        raise
    else:
        session.commit()
```

    2023-02-07 21:56:54,099 INFO sqlalchemy.engine.Engine BEGIN (implicit)
    2023-02-07 21:56:54,102 INFO sqlalchemy.engine.Engine SELECT trabalha.id, trabalha.id_funcionario, trabalha.id_departamento, trabalha.data_entrada, trabalha.data_saida 
    FROM trabalha
    2023-02-07 21:56:54,104 INFO sqlalchemy.engine.Engine [generated in 0.00128s] ()



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">14</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">24</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">27</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">29</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">18</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">28</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">17</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">31</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">12</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">12</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">28</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">13</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">13</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">28</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">4</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">14</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">14</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">25</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">15</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">15</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">16</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">16</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">16</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">17</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">17</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">26</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">18</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">18</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">13</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">19</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">19</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">8</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">6</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">22</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">12</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">20</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">5</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">19</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">11</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2022</span><span style="font-weight: bold">)</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #800080; text-decoration-color: #800080; font-weight: bold">Funcionario</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">id</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #808000; text-decoration-color: #808000">id_funcionario</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">21</span>, <span style="color: #808000; text-decoration-color: #808000">id_departamento</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #808000; text-decoration-color: #808000">data_entrada</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">7</span>/<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2021</span>, <span style="color: #808000; text-decoration-color: #808000">data_saida</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span><span style="font-weight: bold">)</span>
</pre>



    2023-02-07 21:56:54,159 INFO sqlalchemy.engine.Engine COMMIT
