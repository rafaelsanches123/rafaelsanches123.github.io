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
$versao = "1.0" # Variável global
PI = 3.14       # Constante

puts nome
puts $versao
puts PI
```

No Ruby, existem dois tipos principais de variáveis que são cruciais para entender a programação orientada a objetos: __variáveis de instância__ e __variáveis de classe__. Compreender a diferença entre elas é fundamental para escrever código Ruby eficaz. 

**Nesse momento não se preocupe pois vamos nos aprofundar nesse assunto no post referente a Orientação a Objetos em Ruby no decorrer do nosso curso**.

**Variáveis de Instância (@)**
- **Definição**: Variáveis de instância são específicas para cada objeto (instância) de uma classe. Cada vez que você cria um novo objeto a partir de uma classe, esse objeto terá seu próprio conjunto de variáveis de instância.
- **Escopo**: O escopo de uma variável de instância é limitado ao objeto individual ao qual ela pertence. Isso significa que o valor de uma variável de instância pode ser diferente para cada objeto da mesma classe.
- **Declaração**: Variáveis de instância são declaradas usando um único caractere @ antes do nome da variável (por exemplo, @nome, @idade).
- **Uso**: Elas são usadas para armazenar informações que são únicas para cada objeto. Pense nelas como os atributos de um objeto.
- **Exemplo**: Imagine uma classe Cachorro. Cada cachorro tem um nome e uma raça diferentes.  @nome e @raca seriam variáveis de instância porque cada objeto Cachorro teria seu próprio nome e raça.

**Variáveis de Classe (@@)**:
- **Definição**: Variáveis de classe pertencem à própria classe e são compartilhadas por todos os objetos (instâncias) dessa classe. Existe apenas uma cópia de uma variável de classe, que é compartilhada por todas as instâncias da classe e até mesmo por subclasses.
- **Escopo**: O escopo de uma variável de classe é a classe e todas as suas instâncias. Se você modificar o valor de uma variável de classe, a alteração será refletida em todos os objetos daquela classe.
- **Declaração**: Variáveis de classe são declaradas usando dois caracteres @@ antes do nome da variável (por exemplo, @@numero_de_cachorros).
- **Uso**: Elas são usadas para armazenar informações que são comuns a todos os objetos de uma classe, ou para rastrear informações sobre a própria classe.
- **Exemplo**: Usando a classe Cachorro novamente, você poderia ter uma variável de classe @@total_cachorros para rastrear o número total de objetos Cachorro que foram criados. Cada vez que um novo objeto Cachorro é criado, você poderia incrementar @@total_cachorros. Este valor seria compartilhado por todos os objetos Cachorro.

Em resumo:

| Característica   | Variável de Instância (@)            | Variável de Classe (@@)                             |
|------------------|--------------------------------------|-----------------------------------------------------|
| A quem pertence  | Objeto (instância)                   | Classe                                              |
| Compartilhamento | Não compartilhado (único por objeto) | Compartilhado por todos os objetos e subclasses     |
| Uso principal    | Atributos únicos do objeto           | Informações comuns à classe, rastreamento de classe |
| Declaração       | @nome_variavel                       | @@nome_variavel                                     |

Exemplo:  
```ruby
class Cachorro
  @@total_cachorros = 0 # Variável de classe para rastrear o número total de cachorros

  def initialize(nome, raca)
    @nome = nome         # Variável de instância para o nome do cachorro
    @raca = raca         # Variável de instância para a raça do cachorro
    @@total_cachorros += 1 # Incrementa a variável de classe cada vez que um cachorro é criado
  end

  # Método para acessar a variável de instância @nome
  def nome_cachorro
    @nome
  end

  # Método para acessar a variável de instância @raca
  def raca_cachorro
    @raca
  end

  # Método de classe para acessar a variável de classe @@total_cachorros
  def self.total_cachorros
    @@total_cachorros
  end

  # Método para exibir informações do cachorro, incluindo variáveis de instância e de classe
  def exibir_info
    puts "Nome do cachorro: #{@nome}"
    puts "Raça do cachorro: #{@raca}"
    puts "Total de cachorros criados até agora: #{@@total_cachorros}"
    puts "---"
  end
end

cachorro1 = Cachorro.new("Rex", "Labrador") # Criando instâncias da classe Cachorro (objetos cachorro)
cachorro1.exibir_info # Exibindo informações de cada cachorro
cachorro2 = Cachorro.new("Nina", "Poodle") 
cachorro2.exibir_info
cachorro3 = Cachorro.new("Max", "Bulldog")
cachorro3.exibir_info

# Exibindo o total de cachorros usando o método de classe
puts "Número total de cachorros criados (acessado diretamente da classe): #{Cachorro.total_cachorros}"
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

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula - [Saída e Entrada de Dados]({% link  _posts/2025-03-13-curso-de-ruby-saida-e-entrada-de-dados.markdown %})**
