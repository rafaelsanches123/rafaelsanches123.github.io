---
layout: post
title:  "Curso de Ruby - Manipulação de Strings"
date:   2025-03-16 13:45:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

#  **Manipulação de Strings**
As **strings** em Ruby são muito poderosas e oferecem diversos métodos úteis para manipulação de texto.

## **Criando Strings**
```ruby
str1 = "Olá, mundo!"
str2 = 'Ruby é incrível!'
```

Podemos usar **interpolação** para incluir variáveis dentro de strings **(somente com aspas duplas `" "`)**:

```ruby
nome = "Rafael"
puts "Olá, #{nome}!"  # ✅ Funciona
puts 'Olá, #{nome}!'  # ❌ Não funciona (exibe #{nome} como texto)
```

 **Saída:**  
```
Olá, Rafael!
Olá, #{nome}!
```

---

## **Métodos Úteis para Strings**
###  **Letras em Maiúsculas e Minúsculas**
```ruby
str = "Ruby é incrível!"
# Toda a string fica em maiúscula
puts str.upcase   # "RUBY É INCRÍVEL!"
# Toda a string fica em minúscula
puts str.downcase # "ruby é incrível!" 
# A primeira letra fica em maiúscula
puts str.capitalize # "Ruby é incrível!"
```

###  **Removendo Espaços Extras**
```ruby
str = "   Olá, Ruby!   "
puts str.strip  # "Olá, Ruby!"
```

###  **Substituindo Caracteres**
```ruby
str = "Eu amo Java!"
puts str.gsub("Java", "Ruby")  # "Eu amo Ruby!"
```

###  **Dividindo Strings**
```ruby
frase = "Aprender Ruby é divertido"
palavras = frase.split(" ")
puts palavras.inspect  # ["Aprender", "Ruby", "é", "divertido"]
```

###  **Concatenando Strings**
```ruby
nome = "Rafael"
puts "Olá, " + nome + "!"      # Usando +
puts "Olá, #{nome}!"           # Usando interpolação
puts ["Olá", nome, "!"].join(" ") # Usando join
```

###  **Saber o número de caracteres da string**
```ruby
# use os métodos length ou size
"Olá".length  # => 3
```

###  **Inverter uma string**
```ruby
"olá".reverse  # => "álo"
```

###  **Verificar se a string contém uma substring**
```ruby
substring = "l"
"olá".include?(substring)  # => true
```

---

# **Manipulação de Arrays**
Os **arrays** em Ruby são listas dinâmicas que podem armazenar qualquer tipo de dado.

## **Criando Arrays**
```ruby
numeros = [1, 2, 3, 4, 5]
nomes = ["Ana", "João", "Carlos"]
```

Podemos acessar elementos pelo **índice (começando em 0)**:
```ruby
puts nomes[0] # "Ana"
puts nomes[-1] # "Carlos" (último elemento)
```

---

## **Métodos Úteis para Arrays**
###  **Adicionando Elementos**
```ruby
numeros << 6         # Adiciona 6 ao final
numeros.push(7)      # Outra forma de adicionar ao final
numeros.unshift(0)   # Adiciona 0 no início
```
 **Resultado:** `[0, 1, 2, 3, 4, 5, 6, 7]`

---

###  **Removendo Elementos**
```ruby
numeros.pop      # Remove o último elemento
numeros.shift    # Remove o primeiro elemento
numeros.delete(3) # Remove todas as ocorrências do número 3
```

---

###  **Iterando sobre Arrays**
Podemos percorrer um array com `.each`:
```ruby
numeros = [1, 2, 3, 4, 5]

numeros.each do |num|
  puts "Número: #{num}"
end
```
 **Saída:**
```
Número: 1
Número: 2
Número: 3
Número: 4
Número: 5
```

---

###  **Filtrando e Modificando Arrays**
```ruby
pares = numeros.select { |num| num.even? } # Apenas os números pares
puts pares.inspect # [2, 4]

dobrados = numeros.map { |num| num * 2 } # Multiplica cada número por 2
puts dobrados.inspect # [2, 4, 6, 8, 10]
```

Para conhecer outros métodos não ensinados nesse post sobre manipulação de strings você pode consultar [Documentação Oficial sobre Strings do Ruby](https://docs.ruby-lang.org/en/3.4/String.html)

---

#  **Exercícios**
Agora é sua vez! 💪  

1️⃣ Crie um programa que peça ao usuário para digitar uma **frase** e depois exiba a mesma frase, mas com **todas as letras maiúsculas**.  
2️⃣ Dado um array de números `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`, exiba apenas os **números pares**.  
3️⃣ Dado um array de palavras `["ruby", "é", "muito", "legal"]`, transforme todas as palavras em **maiúsculas** e junte-as em uma única string separada por espaço.  

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula em construção!!! - Tratamento de Exceções**