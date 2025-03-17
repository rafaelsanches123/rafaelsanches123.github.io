---
layout: post
title:  "Curso de Ruby - Programação Orientada a Objetos em Ruby"
date:   2025-03-17 15:00:00 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

Nesse post vamos aprender sobre **Classes e Objetos** em Ruby, que são os pilares da **Programação Orientada a Objetos (POO)**. Ruby é uma linguagem completamente orientada a objetos, o que significa que tudo em Ruby é um objeto, incluindo números e até mesmo classes.

---

##  **O que é uma Classe?**
Uma **classe** é como um **modelo** ou **plano de construção** para criar objetos. Uma classe define as propriedades e comportamentos (métodos) que os objetos dessa classe terão. Ela pode ser vista como um molde, enquanto os objetos são as instâncias dessa classe.

### Sintaxe Básica para Definir uma Classe
```ruby
class NomeDaClasse
  # Definindo atributos (variáveis de instância)
  def initialize(parametros)
    @atributo1 = parametros
  end

  # Métodos (comportamentos) da classe
  def nome_do_metodo
    # código
  end
end
```

- **`initialize`** é um método especial chamado **construtor**. Ele é chamado automaticamente sempre que uma nova instância da classe é criada. Os parâmetros passados para `initialize` são usados para inicializar os atributos do objeto.

---

##  **Definindo uma Classe e Criando um Objeto**
Vamos ver um exemplo básico de como criar uma classe e instanciar um objeto dessa classe.

### Exemplo 1: Definindo uma Classe Simples
```ruby
class Pessoa
  def initialize(nome, idade)
    @nome = nome
    @idade = idade
  end

  def saudacao
    "Olá, meu nome é #{@nome} e eu tenho #{@idade} anos."
  end
end

# Criando um objeto (instância) da classe Pessoa
pessoa1 = Pessoa.new("João", 30)
puts pessoa1.saudacao  # Saída: Olá, meu nome é João e eu tenho 30 anos.
```

### Detalhes:
- **`initialize`** define como o objeto será inicializado.
- **`@nome` e `@idade`** são **variáveis de instância**. Elas são exclusivas de cada instância (objeto) da classe.
- **`Pessoa.new("João", 30)`** cria um novo objeto da classe `Pessoa`.

---

##  **Atributos e Métodos**
Dentro de uma classe, você pode ter atributos e métodos.

- **Atributos** são variáveis que armazenam dados dentro de um objeto.
- **Métodos** são funções que definem o comportamento de um objeto.

### Atributos de Leitura e Escrita
Para tornar um atributo acessível (ler ou modificar seu valor) de fora da classe, você pode usar os métodos **getter** e **setter**.

- **Getter**: Método para acessar um atributo.
- **Setter**: Método para modificar um atributo.

### Exemplo 2: Atributos Getter e Setter
```ruby
class Carro
  def initialize(modelo, cor)
    @modelo = modelo
    @cor = cor
  end

  # Getter e Setter para o modelo
  def modelo
    @modelo
  end

  def modelo=(novo_modelo)
    @modelo = novo_modelo
  end

  # Getter e Setter para a cor
  def cor
    @cor
  end

  def cor=(nova_cor)
    @cor = nova_cor
  end
end

# Criando um objeto da classe Carro
carro1 = Carro.new("Fusca", "azul")
puts carro1.modelo  # Saída: Fusca
puts carro1.cor     # Saída: azul

# Alterando os atributos
carro1.modelo = "Civic"
carro1.cor = "preto"

puts carro1.modelo  # Saída: Civic
puts carro1.cor     # Saída: preto
```

---

##  **Métodos de Classe**
Além dos métodos de instância (que pertencem a objetos), podemos criar **métodos de classe**, que pertencem à própria classe e não a instâncias específicas.

### Exemplo 3: Método de Classe
```ruby
class Matematica
  def self.somar(a, b)
    a + b
  end
end

# Chamando o método de classe
puts Matematica.somar(5, 3)  # Saída: 8
```

- **`self.somar`** define um **método de classe**. O `self` se refere à própria classe `Matematica` e não a um objeto específico.

---

##  **Herança**
A **herança** é um conceito central da POO onde uma classe pode herdar comportamentos e atributos de outra classe. Isso permite criar novas classes baseadas em classes existentes, sem duplicar código.

### Exemplo 4: Herança
```ruby
class Animal
  def initialize(nome)
    @nome = nome
  end

  def falar
    "Eu sou um animal."
  end
end

class Cachorro < Animal
  def falar
    "Au Au!"
  end
end

# Criando objetos
animal = Animal.new("Genérico")
cachorro = Cachorro.new("Rex")

puts animal.falar  # Saída: Eu sou um animal.
puts cachorro.falar  # Saída: Au Au!
```

### Detalhes:
- **`Cachorro < Animal`** indica que a classe `Cachorro` herda de `Animal`. 
- A classe `Cachorro` pode sobrescrever o método `falar` para oferecer um comportamento diferente.

---

##  **Polimorfismo**
O **polimorfismo** permite que diferentes classes compartilhem o mesmo nome de método, mas com comportamentos diferentes. Isso é possível através da herança e sobrescrita de métodos.

No exemplo anterior, o método `falar` foi polimórfico, pois o comportamento do método foi diferente para o `Animal` e para o `Cachorro`.

---

##  **Encapsulamento**
O **encapsulamento** é o conceito de ocultar os detalhes internos de uma classe e expor apenas o que é necessário para o uso externo. Em Ruby, isso é feito principalmente usando **métodos de leitura e escrita** para acessar variáveis de instância.

### Exemplo 5: Encapsulamento
```ruby
class ContaBancaria
  def initialize(saldo)
    @saldo = saldo
  end

  def saldo
    @saldo
  end

  def depositar(valor)
    @saldo += valor
  end
end

conta = ContaBancaria.new(100)
conta.depositar(50)
puts conta.saldo  # Saída: 150
```

- **`@saldo`** é uma variável de instância privada.
- O acesso a ela é feito através dos métodos `saldo` e `depositar`, garantindo que o saldo não seja modificado diretamente fora da classe.

---

##  **Exercício**
Agora, pratique criando suas próprias classes e objetos! 💪

1️⃣ Crie uma classe **Pessoa** com os atributos `nome` e `idade`. Implemente um método `falar` que retorna uma saudação usando o nome e a idade da pessoa.  

2️⃣ Crie uma classe **Produto** com os atributos `nome`, `preço` e `quantidade_em_estoque`. Implemente métodos para **adicionar** e **remover** unidades do produto no estoque, além de um método para **calcular o valor total** do estoque (preço * quantidade).

---

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula - [Desafio Final - Jogo das Luzes]({% link _posts/2025-03-17-jogo-das-luzes.markdown %})**