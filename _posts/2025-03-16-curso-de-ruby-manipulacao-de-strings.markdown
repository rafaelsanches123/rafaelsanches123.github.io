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

Para conhecer outros métodos não ensinados nesse post sobre manipulação de strings você pode consultar [Documentação Oficial sobre Strings do Ruby](https://docs.ruby-lang.org/en/3.4/String.html)

---

#  **Exercícios**
Agora é sua vez! 💪  

1. **Concatenação e Interpolação**
**Tarefa:**
    1.  Declare duas variáveis: `primeiro_nome` com o valor "João" e `ultimo_nome` com o valor "Silva".
    2.  Use o operador de concatenação (`+`) para criar uma variável chamada `nome_completo` que contenha o nome completo (lembre-se de adicionar um espaço entre o primeiro e o último nome). Imprima `nome_completo`.
    3.  Declare uma variável `idade` com o valor 30.
    4.  Use a interpolação de strings (com `#{}`) para criar uma frase que diga: "Meu nome completo é [valor de nome_completo] e eu tenho [valor de idade] anos." Imprima essa frase.

2. **Conversão de Caso e Comprimento**
**Tarefa:**
    1.  Declare uma variável chamada `frase_exemplo` com a seguinte frase: "ruby é uma linguagem poderosa".
    2.  Use um método de string para converter toda a `frase_exemplo` para letras maiúsculas. Imprima o resultado.
    3.  Use outro método de string para converter toda a `frase_exemplo` para letras minúsculas. Imprima o resultado (deverá ser a frase original).
    4.  Use um método para encontrar o número de caracteres (incluindo espaços) na `frase_exemplo`. Imprima o comprimento da frase.

3. **Substring e Divisão**
**Tarefa:**
    1.  Declare uma variável chamada `texto` com a seguinte string: "maçã,banana,laranja,uva".
    2.  Use um método para verificar se a string `texto` contém a substring "banana". Imprima o resultado (deverá ser `true`).
    3.  Use um método para encontrar o índice da primeira ocorrência da substring "laranja" na string `texto`. Imprima o índice.
    4.  Use um método para dividir a string `texto` em um array de substrings, usando a vírgula (`,`) como delimitador. Imprima o array resultante.

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula - [Estruturas de Dados]({% link _posts/2025-03-16-curso-de-ruby-estruturas-de-dados.markdown %})**