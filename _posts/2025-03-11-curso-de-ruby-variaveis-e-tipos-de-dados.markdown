---
layout: post
title:  "Curso de Ruby - Variáveis e Tipos de Dados"
date:   2025-03-11 15:55:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }


## **Variáveis em Ruby**
Ruby é uma linguagem **dinamicamente tipada**, o que significa que você **não** precisa declarar o tipo da variável. O interpretador infere automaticamente.  

```ruby
nome = "Rafael"   # String
idade = 30        # Integer
altura = 1.75     # Float
maior_idade = true   # Boolean

puts nome   # Rafael
puts idade  # 30
puts altura # 1.75
puts maior_idade # true
```

---

##  **Convenções de Nomeação de Variáveis**
No Ruby, existem diferentes tipos de variáveis com regras específicas:  

| Tipo de Variável | Exemplo | Descrição |
|------------------|---------|-----------|
| **Variável Local** | `nome = "Rafael"` | Começa com **letra minúscula** ou `_`, acessível apenas no escopo onde foi definida. |
| **Variável de Instância** | `@idade = 30` | Começa com `@`, usada dentro de **classes** para armazenar valores do objeto. |
| **Variável de Classe** | `@@contagem = 0` | Começa com `@@`, usada para armazenar valores compartilhados entre todos os objetos da classe. |
| **Variável Global** | `$pi = 3.14` | Começa com `$`, pode ser acessada de qualquer lugar (⚠️ Evite usar muito). |
| **Constante** | `PI = 3.14` | Começa com **letra maiúscula**, não pode ser alterada (mas Ruby permite um aviso se modificar). |

Exemplo:  
```ruby
nome = "João"  # Variável local
@idade = 25     # Variável de instância
@@contador = 10 # Variável de classe
$versao = "1.0" # Variável global
PI = 3.14       # Constante

puts nome
puts @idade
puts @@contador
puts $versao
puts PI
```

---

## **Tipos de Dados**
### ✅ **Strings (`String`)**
```ruby
nome = "Rafael"
puts nome.upcase    # "RAFAEL"
puts nome.downcase  # "rafael"
puts nome.length    # 6
puts "Olá, #{nome}!"  # Interpolação de string
```

### ✅ **Números Inteiros (`Integer`)**
```ruby
idade = 30
puts idade.class  # Integer
puts idade.next   # 31
puts idade.to_f   # Converte para float
```

### ✅ **Números Decimais (`Float`)**
```ruby
altura = 1.75
puts altura.round(1) # Arredonda para 1 casa decimal
puts altura.to_i     # Converte para inteiro
```

### ✅ **Booleanos (`true` e `false`)**
```ruby
ligado = true
desligado = false
puts ligado && desligado  # false
puts ligado || desligado  # true
puts !ligado              # false (negação)
```

### ✅ **Arrays (`Array`)**
```ruby
numeros = [1, 2, 3, 4, 5]
puts numeros[0]  # Primeiro elemento -> 1
puts numeros.last # Último elemento -> 5

numeros.push(6)   # Adiciona elemento
puts numeros.inspect  # [1, 2, 3, 4, 5, 6]
```

### ✅ **Dicionários (`Hash`)**
```ruby
pessoa = { nome: "Rafael", idade: 30 }
puts pessoa[:nome]  # Rafael
pessoa[:altura] = 1.75  # Adicionando novo dado
puts pessoa.inspect
```

---

## **Conversão de Tipos**
### 🔄 **Convertemos valores com `.to_s`, `.to_i`, `.to_f`, `.to_a`, etc.**
```ruby
num = "42"
puts num.to_i   # Converte para inteiro -> 42

decimal = 3.14
puts decimal.to_s  # Converte para string -> "3.14"

lista = "1,2,3".split(",")  # ["1", "2", "3"]
puts lista.inspect
```

---

## **Exercícios**
Agora, pratique resolvendo estes desafios:  
1️⃣ Crie uma variável `nome` e atribua seu nome a ela. Em seguida, exiba `"Olá, [nome]!"`.  
2️⃣ Crie uma variável e atribua a ela um número em formato de string e depois converta-o para inteiro. Multiplique por 2 e exiba o resultado.  
3️⃣ Crie um `Hash` para armazenar **nome, idade e cidade** de uma pessoa e exiba as informações.

**Se quiser, tente resolver e envie nos comentários suas respostas para analisarmos juntos!** 🚀

**Próxima aula em construção!!! - Saída e Entrada de Dados**