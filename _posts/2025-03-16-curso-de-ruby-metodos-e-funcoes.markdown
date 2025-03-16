---
layout: post
title:  "Curso de Ruby - Métodos (Funções)"
date:   2025-03-16 10:45:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

## **O que são Métodos?**

Métodos são blocos de código reutilizáveis que realizam **uma tarefa específica**.  

Eles ajudam a **organizar e reutilizar código**.  

```ruby
def saudacao
  puts "Olá, seja bem-vindo!"
end

saudacao  # Chamando o método
```
**Saída:**  
```
Olá, seja bem-vindo!
```

---

## **Métodos com Parâmetros**
Podemos passar **valores (parâmetros)** para personalizar o método.  

```ruby
def saudacao(nome)
  puts "Olá, #{nome}!"
end

saudacao("Rafael")
saudacao("Maria")
```
**Saída:**  
```
Olá, Rafael!
Olá, Maria!
```

---

## **Métodos com Retorno (`return`)**
O `return` permite que o método **devolva um valor**.  

```ruby
def soma(a, b)
  return a + b
end

resultado = soma(5, 3)
puts "O resultado é #{resultado}"
```
**Saída:**  
```
O resultado é 8
```

ℹ️ **Dica:** Em Ruby, o `return` é opcional, pois um método **retorna automaticamente o último valor calculado**.  
```ruby
def soma(a, b)
  a + b  # Retorno implícito
end
```

---

## **Parâmetros Opcionais**
Podemos definir **valores padrão** para os parâmetros.  

```ruby
def saudacao(nome = "Visitante")
  puts "Olá, #{nome}!"
end

saudacao       # Usa o valor padrão
saudacao("Ana") # Usa o valor passado
```
**Saída:**  
```
Olá, Visitante!
Olá, Ana!
```

---

## **Métodos com Vários Argumentos (`*args`)**
Podemos usar `*args` para passar **um número variável de argumentos**.  

```ruby
def soma(*numeros)
  numeros.sum
end

puts soma(1, 2, 3, 4)  # Soma 1+2+3+4 = 10
puts soma(10, 20)      # Soma 10+20 = 30
```
**Saída:**  
```
10
30
```

---

## **Métodos como Expressões (`lambda` e `proc`)**
Em Ruby, podemos criar funções anônimas com `lambda` ou `proc`.  

### **Exemplo com `lambda`**
```ruby
multiplica = ->(a, b) { a * b }
puts multiplica.call(3, 4)
```
**Saída:**  
```
12
```

### **Exemplo com `proc`**
```ruby
soma = Proc.new { |a, b| a + b }
puts soma.call(5, 2)
```
**Saída:**  
```
7
```

---

## **Exercícios**
Agora é sua vez! 💪  

1. **Crie um método** que recebe um número e retorna se ele é **par ou ímpar**.  
2. **Escreva um método** que recebe um nome e imprime `"Olá, [nome]!"`, mas se não for passado nenhum nome, ele deve exibir `"Olá, Visitante!"`.  
3. **Crie um método** que recebe **vários números** e retorna a **soma deles**.  
4. Crie um programa que liste para o usuário as seguintes opções na tela: 1 - soma, 2 - subtração, 3 - multiplicação, 4 - divisão e 5 - Sair. Capture a opção (entrada) desejada pelo usuário e em seguida de acordo com a opção desejada implemente uma função que solicite 2 números para cada opção que ele escolher e retorne o resultado do primeiro número com o segundo número da opção escolhida na tela. Quando o usuário digitar a opção 5 o seu programa precisa ser finalizado e parar a execução.

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula em construção!!! - Manipulação de Strings**