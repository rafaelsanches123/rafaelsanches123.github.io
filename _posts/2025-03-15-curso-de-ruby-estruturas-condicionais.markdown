---
layout: post
title:  "Curso de Ruby - Estruturas Condicionais"
date:   2025-03-15 09:30:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

## **Estrutura `if` e `else`**
O `if` é usado para **executar um bloco de código caso a condição seja verdadeira**.  
Se a condição for **falsa**, o código dentro do `else` será executado (caso tenha).  

```ruby
idade = 18

if idade >= 18
  puts "Você pode dirigir!"
else
  puts "Você ainda não pode dirigir!"
end
```
**Saída:**  
```
Você pode dirigir!
```

---

## **`elsif` (Várias Condições)**
Usamos `elsif` para testar **várias condições**.  

```ruby
nota = 7

if nota >= 9
  puts "Excelente!"
elsif nota >= 7
  puts "Bom!"
elsif nota >= 5
  puts "Recuperação!"
else
  puts "Reprovado!"
end
```
**Saída:**  
```
Bom!
```

---

## **Operador Ternário (`?`)**
O operador ternário é uma forma **mais curta** de escrever um `if/else`.  

```ruby
idade = 20
mensagem = idade >= 18 ? "Maior de idade" : "Menor de idade"
puts mensagem
```
**Saída:**  
```
Maior de idade
```

---

## **`unless` (Executa se a Condição for Falsa)**
O `unless` é o oposto de `if`. Ele executa o código **se a condição for falsa**.  

```ruby
idade = 15

unless idade >= 18
  puts "Você não pode votar ainda!"
end
```
**Saída:**  
```
Você não pode votar ainda!
```

---

## **`case` (Switch Case no Ruby)**
O `case` é útil para **evitar múltiplos `if/elsif`**.  

```ruby
dia = "segunda"

case dia
when "segunda"
  puts "Início da semana!"
when "sexta"
  puts "Quase final de semana!"
when "domingo"
  puts "Dia de descanso!"
else
  puts "Dia comum!"
end
```
**Saída:**  
```
Início da semana!
```

---

## **Operadores de Comparação**

| Operador | Descrição | Exemplo |
|----------|------------|---------|
| `==` | Igualdade | `5 == 5` → `true` |
| `!=` | Diferente | `5 != 3` → `true` |
| `>` | Maior que | `7 > 4` → `true` |
| `<` | Menor que | `3 < 8` → `true` |
| `>=` | Maior ou igual | `10 >= 10` → `true` |
| `<=` | Menor ou igual | `2 <= 5` → `true` |

---

## **Operadores Lógicos**

| Operador 	| Descrição 	| Exemplo 	|
|:---:	|:---:	|:---:	|
| __and__ 	| Retorna true se ambas as expressões forem true. Caso contrário, false. 	| idade > 18 __and__ possui_carteira (será true se idade for maior que 18 e possui_carteira for true) 	|
| __&&__ 	| Sinônimo de and. 	| temperatura > 25 __&&__ umidade < 60 (será true se temperatura for maior que 25 e umidade for menor que 60) 	|
| __or__ 	| Retorna true se pelo menos uma das expressões for true. Retorna false somente se ambas forem false. 	| dia == "sábado" __or__ dia == "domingo" (será true se dia for "sábado" ou "domingo") 	|
| __\|\|__ 	| Sinônimo de or. 	| dia == "sábado" __\|\|__ dia == "domingo" (será true se dia for "sábado" ou "domingo") 	|
| __not__ 	| Retorna true se a expressão for false, e false se a expressão for true. 	| __not__ usuario_logado (será true se usuario_logado for false) 	|
| __!__ 	| Sinônimo de not. 	| __!arquivo_existe__ (será true se arquivo_existe for false) 	|

Exemplo:
```ruby
idade = 20
tem_habilitacao = true

if idade >= 18 && tem_habilitacao
  puts "Pode dirigir!"
else
  puts "Não pode dirigir!"
end
```

---

## **Exercícios**
Agora é sua vez! 💪

1️⃣ Peça para o usuário digitar sua idade e exiba se ele é **maior ou menor de idade**.  
2️⃣ Solicite uma **nota** e diga se o aluno está **aprovado (>= 7), em recuperação (>= 5) ou reprovado**.  
3️⃣ Pergunte um **número de 1 a 7** e diga qual o dia da semana correspondente.  

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀


**Próxima aula em construção!!! - Estruturas de Repetição (loops)**