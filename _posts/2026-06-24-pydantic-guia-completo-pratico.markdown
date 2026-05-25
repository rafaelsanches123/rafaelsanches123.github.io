--- 
layout: post
title: "Pydantic: Validação de Dados Moderna em Python com Exemplos Práticos"
date: 2026-05-24 09:00:00 -0300
categories: pydantic validação python dados engenharia arquitetura software
---

![Pydantic]({{ site.url }}/assets/pydantic.png){:style="width: 100%" }

## Introdução

Quando trabalhamos com APIs, pipelines de dados, aplicações web, automações ou sistemas distribuídos em Python, uma das maiores dores é garantir que os dados recebidos estejam corretos.

Imagine alguns cenários:

* Um usuário envia um e-mail inválido.
* Uma API retorna um campo nulo inesperado.
* Um pipeline recebe uma string onde deveria existir um número.
* Um microserviço envia dados incompletos.

Esses problemas podem gerar falhas silenciosas, erros difíceis de rastrear e até inconsistências graves no sistema.

É exatamente nesse contexto que o **Pydantic** se tornou uma das bibliotecas mais importantes do ecossistema Python moderno.

O Pydantic permite:

* Validar dados automaticamente
* Converter tipos automaticamente
* Garantir consistência de entrada
* Facilitar integração com APIs
* Criar modelos fortemente tipados
* Reduzir código boilerplate
* Melhorar a legibilidade e manutenção do código

Hoje o Pydantic é amplamente utilizado em frameworks e plataformas como:

* FastAPI
* LangChain
* CrewAI
* Sistemas de IA
* Engenharia de Dados
* Microsserviços
* ETL e pipelines

Neste artigo vamos aprender:

* O que é Pydantic
* Como instalar
* Como criar modelos
* Como validar dados
* Conversão automática de tipos
* Campos opcionais
* Validators
* Nested Models
* Serialização
* Configurações avançadas
* Exemplos reais e práticos


# O que é o Pydantic?

O Pydantic é uma biblioteca Python utilizada para:

* Validação de dados
* Parsing de dados
* Conversão de tipos
* Definição de schemas

Ele utiliza as famosas **Type Hints** do Python.

Exemplo:

```python
nome: str
idade: int
```

A partir dessas definições, o Pydantic valida automaticamente os dados.


# Instalação

## Instalando com pip

```bash
pip install pydantic
```

## Verificando instalação

```python
import pydantic

print(pydantic.__version__)
```



# Primeiro Exemplo

Vamos criar nosso primeiro modelo.

```python
from pydantic import BaseModel

class Usuario(BaseModel):
    nome: str
    idade: int

usuario = Usuario(
    nome="Rafael",
    idade=30
)

print(usuario)
```

Saída:

```python
nome='Rafael' idade=30
```

# Conversão Automática de Tipos

Um dos recursos mais interessantes do Pydantic é o parsing automático.

```python
from pydantic import BaseModel

class Produto(BaseModel):
    nome: str
    preco: float
    quantidade: int

produto = Produto(
    nome="Notebook",
    preco="5999.90",
    quantidade="10"
)

print(produto)
print(type(produto.preco))
print(type(produto.quantidade))
```

Saída:

```python
nome='Notebook' preco=5999.9 quantidade=10
<class 'float'>
<class 'int'>
```

Mesmo enviando strings, o Pydantic converte automaticamente.


# Tratamento de Erros

Agora vamos provocar um erro.

```python
from pydantic import BaseModel

class Pessoa(BaseModel):
    nome: str
    idade: int

pessoa = Pessoa(
    nome="Maria",
    idade="vinte"
)
```

Saída:

```python
ValidationError: 1 validation error for Pessoa
idade
  Input should be a valid integer
```

O Pydantic gera mensagens extremamente detalhadas.

Isso é excelente para:

* APIs
* Logs
* Debug
* Sistemas distribuídos



# Campos Opcionais

Nem todos os campos precisam ser obrigatórios.

```python
from typing import Optional
from pydantic import BaseModel

class Cliente(BaseModel):
    nome: str
    email: Optional[str] = None

cliente = Cliente(nome="João")

print(cliente)
```

Saída:

```python
nome='João' email=None
```



# Valores Padrão

```python
from pydantic import BaseModel

class Pedido(BaseModel):
    status: str = "PENDENTE"
    valor: float

pedido = Pedido(valor=150.0)

print(pedido)
```

Saída:

```python
status='PENDENTE' valor=150.0
```



# Validação com Email

O Pydantic possui tipos especiais.

```bash
pip install email-validator
```

Exemplo:

```python
from pydantic import BaseModel, EmailStr

class Usuario(BaseModel):
    nome: str
    email: EmailStr

usuario = Usuario(
    nome="Rafael",
    email="rafael@email.com"
)

print(usuario)
```

Agora um exemplo inválido:

```python
usuario = Usuario(
    nome="Rafael",
    email="email_invalido"
)
```

Saída:

```python
ValidationError: value is not a valid email address
```



# Validators Personalizados

Você pode criar suas próprias regras.

## Exemplo: validar idade mínima

```python
from pydantic import BaseModel, field_validator

class Usuario(BaseModel):
    nome: str
    idade: int

    @field_validator("idade")
    @classmethod
    def validar_idade(cls, value):
        if value < 18:
            raise ValueError("Usuário deve ser maior de idade")
        return value

usuario = Usuario(
    nome="Carlos",
    idade=25
)

print(usuario)
```

Agora um caso inválido:

```python
usuario = Usuario(
    nome="Pedro",
    idade=15
)
```

Saída:

```python
ValidationError: Usuário deve ser maior de idade
```



# Nested Models

O Pydantic suporta objetos aninhados.

## Exemplo com Endereço

```python
from pydantic import BaseModel

class Endereco(BaseModel):
    rua: str
    cidade: str
    estado: str

class Usuario(BaseModel):
    nome: str
    endereco: Endereco

usuario = Usuario(
    nome="Rafael",
    endereco={
        "rua": "Rua A",
        "cidade": "São Paulo",
        "estado": "SP"
    }
)

print(usuario)
```

Saída:

```python
nome='Rafael' endereco=Endereco(rua='Rua A', cidade='São Paulo', estado='SP')
```



# Trabalhando com Listas

```python
from typing import List
from pydantic import BaseModel

class Pedido(BaseModel):
    produtos: List[str]

pedido = Pedido(
    produtos=["Notebook", "Mouse", "Teclado"]
)

print(pedido)
```



# Serialização JSON

Transformar objetos em JSON é extremamente comum.

```python
from pydantic import BaseModel

class Produto(BaseModel):
    nome: str
    preco: float

produto = Produto(
    nome="Notebook",
    preco=4500
)

print(produto.model_dump())
print(produto.model_dump_json())
```

Saída:

```python
{'nome': 'Notebook', 'preco': 4500.0}
{"nome":"Notebook","preco":4500.0}
```



# Alias de Campos

Muito útil quando APIs utilizam nomes diferentes.

```python
from pydantic import BaseModel, Field

class Usuario(BaseModel):
    nome_completo: str = Field(alias="full_name")

usuario = Usuario(full_name="Rafael Sanches")

print(usuario)
```



# Configurações do Modelo

## Exemplo: bloquear campos extras

```python
from pydantic import BaseModel, ConfigDict

class Usuario(BaseModel):
    model_config = ConfigDict(extra="forbid")

    nome: str

usuario = Usuario(
    nome="Rafael",
    idade=30
)
```

Saída:

```python
ValidationError: Extra inputs are not permitted
```



# Exemplo Real: API com FastAPI

O FastAPI utiliza Pydantic internamente.

## Instalação

```bash
pip install fastapi uvicorn
```

## Exemplo Completo

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Usuario(BaseModel):
    nome: str
    email: str
    idade: int

@app.post("/usuarios")
def criar_usuario(usuario: Usuario):
    return {
        "mensagem": "Usuário criado com sucesso",
        "dados": usuario
    }
```

Executando:

```bash
uvicorn main:app --reload
```

Agora o FastAPI:

* valida automaticamente
* gera documentação
* cria schemas
* valida JSON
* retorna erros estruturados



# Exemplo Prático: Pipeline de Dados

Imagine um pipeline recebendo dados CSV.

```python
from pydantic import BaseModel

class Venda(BaseModel):
    produto: str
    valor: float
    quantidade: int

registro = {
    "produto": "Notebook",
    "valor": "5000",
    "quantidade": "2"
}

venda = Venda(**registro)

print(venda)
```

Isso ajuda muito em:

* Data Engineering
* ETL
* Data Quality
* APIs
* Integração de sistemas



# Exemplo Prático: IA e Multiagentes

Hoje muitas aplicações de IA usam Pydantic.

Exemplo simples:

```python
from pydantic import BaseModel

class RespostaIA(BaseModel):
    titulo: str
    resumo: str
    score: float
```

Isso permite:

* Estruturar respostas
* Garantir consistência
* Validar outputs de LLMs
* Integrar agentes

Ferramentas como:

* LangChain
* CrewAI
* AutoGen
* LlamaIndex

utilizam bastante Pydantic.



# Diferença entre Dataclass e Pydantic

## Dataclass

```python
from dataclasses import dataclass

@dataclass
class Usuario:
    nome: str
    idade: int
```

Dataclass:

* Organiza dados
* Não valida automaticamente

## Pydantic

```python
from pydantic import BaseModel

class Usuario(BaseModel):
    nome: str
    idade: int
```

Pydantic:

* Organiza dados
* Valida dados
* Converte tipos
* Gera erros estruturados



# Principais Benefícios do Pydantic

## 1. Código mais seguro

Menos bugs relacionados a tipos.

## 2. APIs mais robustas

Validação automática.

## 3. Melhor manutenção

Schemas claros.

## 4. Excelente integração

Funciona perfeitamente com:

* FastAPI
* IA
* Engenharia de Dados
* Microsserviços

## 5. Redução de boilerplate

Menos código manual.



# Boas Práticas

## Utilize Type Hints corretamente

```python
nome: str
idade: int
ativo: bool
```

## Crie modelos pequenos

Evite modelos gigantes.

## Reutilize modelos

```python
class Endereco(BaseModel):
    ...
```

## Valide regras de negócio

Use validators.

## Evite lógica excessiva dentro dos modelos

Mantenha foco em validação.



# Quando Utilizar Pydantic?

O Pydantic é excelente para:

* APIs REST
* Microsserviços
* Engenharia de Dados
* Data Mesh
* IA Generativa
* Sistemas Multiagentes
* ETL
* Processamento de eventos
* Integração entre sistemas
* Automação



# Conclusão

O Pydantic se tornou praticamente um padrão no ecossistema Python moderno.

Ele resolve um problema extremamente comum:

> garantir que os dados estejam corretos.

Além disso, ele torna o código:

* Mais limpo
* Mais seguro
* Mais legível
* Mais profissional

Se você trabalha com:

* FastAPI
* IA
* Engenharia de Dados
* APIs
* Microsserviços
* ETL

aprender Pydantic é praticamente obrigatório.



# Próximos Passos

Agora que você conhece os fundamentos do Pydantic, experimente:

* Criar APIs com FastAPI
* Validar dados de pipelines
* Integrar com CrewAI
* Criar modelos para IA
* Estruturar outputs de LLMs
* Construir validações avançadas



# Desafio Prático

Crie um sistema simples de cadastro de produtos usando Pydantic com:

* Nome
* Preço
* Quantidade
* Categoria
* Validação de preço positivo
* Validação de estoque mínimo

Depois tente:

* Converter para API FastAPI
* Persistir em banco
* Criar testes automatizados


### Gostou do conteúdo?