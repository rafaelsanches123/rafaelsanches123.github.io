---
layout: post
title:  "Curso de Ruby - Estruturas de Repetição (loops)"
date:   2025-03-15 10:45:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

## **`while` (Enquanto a condição for verdadeira)**
O loop `while` executa um bloco de código **enquanto a condição for verdadeira**.  

```ruby
contador = 1

while contador <= 5
  puts "Número: #{contador}"
  contador += 1
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

## **`until` (Enquanto a condição for falsa)**
O `until` é o oposto do `while`: **ele executa enquanto a condição for falsa**.  

```ruby
contador = 1

until contador > 5
  puts "Número: #{contador}"
  contador += 1
end
```
**Saída:** (igual ao `while`)  
```
Número: 1
Número: 2
Número: 3
Número: 4
Número: 5
```

---

## **`for` (Loop com Intervalo Específico)**
O `for` é útil para percorrer um **intervalo de valores** ou **arrays**.  

```ruby
for i in 1..5
  puts "Número: #{i}"
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

## **`.times` (Executa um bloco várias vezes)**
O método `.times` repete um bloco **um número fixo de vezes**.  

```ruby
5.times do |i|
  puts "Executando pela #{i + 1}ª vez"
end
```
**Saída:**  
```
Executando pela 1ª vez
Executando pela 2ª vez
Executando pela 3ª vez
Executando pela 4ª vez
Executando pela 5ª vez
```

---

## **`loop do` (Loop Infinito)**
O `loop do` cria um **loop infinito** (só para quando usamos `break`).  

```ruby
contador = 1

loop do
  puts "Número: #{contador}"
  contador += 1
  break if contador > 5
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

## **`each` (Percorrer Arrays e Hashes)**
O `.each` é muito usado para percorrer **arrays e hashes**.  

### **Percorrendo um Array**
```ruby
numeros = [1, 2, 3, 4, 5]

numeros.each do |num|
  puts "Número: #{num}"
end
```

### **Percorrendo um Hash**
```ruby
pessoa = { nome: "Rafael", idade: 30 }

pessoa.each do |chave, valor|
  puts "#{chave}: #{valor}"
end
```
**Saída:**  
```
nome: Rafael
idade: 30
```

---

## **Controlando Loops (`break` e `next`)**
### **`break` (Interrompe o Loop)**
```ruby
10.times do |i|
  break if i == 5
  puts i
end
```
**Saída:**  
```
0
1
2
3
4
```

### **`next` (Pula para a Próxima Iteração)**
```ruby
10.times do |i|
  next if i.even? # Pula números pares
  puts i
end
```
**Saída:**  
```
1
3
5
7
9
```

---

## **Exercícios**

Agora é sua vez! 💪  

1️⃣ Escreva um programa que imprima os números de **1 a 10** usando `while`.  
2️⃣ Crie um loop que peça um número ao usuário **até que ele digite 0**. Depois digitar **0** o loop deve terminar.  
3️⃣ Crie um **array de números** inteiros, percorra-o com `.each` e exiba apenas os números **pares**.

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula em construção!!! - [Métodos (Funções)]({% link _posts/2025-03-16-curso-de-ruby-metodos-e-funcoes.markdown %})**
