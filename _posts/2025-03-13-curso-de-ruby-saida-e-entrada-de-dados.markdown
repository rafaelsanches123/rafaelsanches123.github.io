---
layout: post
title:  "Curso de Ruby - Saída e Entrada de Dados"
date:   2025-03-13 10:30:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

## **Saída de Dados (`puts`, `print` e `p`)**  
Em Ruby, podemos exibir informações na tela usando diferentes métodos.  

### ✅ **`puts` (Output + Quebra de Linha)**  
Exibe o texto e adiciona automaticamente uma **quebra de linha** no final.  
```ruby
puts "Olá, mundo!"
puts "Bem-vindo ao Ruby!"
```
**Saída:**  
```
Olá, mundo!
Bem-vindo ao Ruby!
```

---

### ✅ **`print` (Output Sem Quebra de Linha)**  
Diferente de `puts`, `print` não adiciona uma quebra de linha automática.  
```ruby
print "Olá, "
print "mundo!"
```
**Saída:**  
```
Olá, mundo!
```

---

### ✅ **`p` (Imprime e Mostra o Tipo Real do Objeto)**  
O `p` é útil para depuração, pois exibe o valor como ele é armazenado na memória.  
```ruby
texto = "  Ruby  "
puts texto      # Ruby (removendo espaços automaticamente)
p texto         # "  Ruby  " (mantém espaços e aspas)
```

---

## **Entrada de Dados (`gets.chomp`)**
Para capturar dados do usuário, usamos `gets`.  

### ✅ **Capturando Entrada do Usuário**  
```ruby
puts "Digite seu nome:"
nome = gets.chomp  # `chomp` remove a quebra de linha
puts "Olá, #{nome}!"
```
**Exemplo de Entrada/Saída:**  
```
Digite seu nome:
Rafael
Olá, Rafael!
```

---

## **Convertendo Entradas**
Como tudo digitado pelo usuário via `gets` é tratado como **string**, precisamos converter quando necessário.  

### ✅ **Convertendo para Inteiro (`to_i`)**
```ruby
puts "Digite sua idade:"
idade = gets.chomp.to_i  # Converte para inteiro
puts "Daqui a 5 anos, você terá #{idade + 5} anos!"
```

### ✅ **Convertendo para Float (`to_f`)**
```ruby
puts "Digite sua altura:"
altura = gets.chomp.to_f  # Converte para número decimal
puts "Sua altura em centímetros é #{altura * 100} cm"
```

---

## **Exercícios**
Agora é sua vez! 💪  

1️⃣ Peça para o usuário digitar seu **nome** e exiba `"Bem-vindo, [nome]!"`.  
2️⃣ Solicite um **número**, converta para **inteiro**, multiplique por 3 e mostre o resultado.  
3️⃣ Peça para o usuário digitar um **número decimal** e exiba o dobro dele.  

**Se quiser, tente resolver e envie nos comentários suas respostas para analisarmos juntos!** 🚀


**Próxima aula em construção!!! - Estruturas Condicionais**