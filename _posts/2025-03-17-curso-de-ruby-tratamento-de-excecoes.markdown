---
layout: post
title:  "Curso de Ruby - Tratamento de Exceções"
date:   2025-03-17 10:45:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

O tratamento de erros é fundamental para garantir que seu programa lide com situações inesperadas de forma controlada, sem travar.

##  **O que são Exceções?**
Exceções são **erros** que ocorrem durante a execução do programa. Quando uma exceção é levantada (ou seja, ocorre um erro), ela interrompe o fluxo normal do programa. No entanto, podemos **capturar** essas exceções e tratá-las de maneira adequada para evitar que o programa falhe.

---

##  **Como Funciona o Tratamento de Exceções em Ruby?**
Ruby utiliza os blocos `begin`, `rescue`, `else`, e `ensure` para tratar erros. A estrutura básica de tratamento de exceções é:

```ruby
begin
  # Código que pode gerar erro
rescue TipoDeErro => e
  # Código que trata o erro
else
  # Código que é executado se não houver erro
ensure
  # Código que é sempre executado, independentemente de erro
end
```

### Componentes:

- **`begin`**: Inicia o bloco de código onde o erro pode ocorrer.
- **`rescue`**: Captura o erro e permite tratá-lo.
- **`else`**: (Opcional) Executado se **nenhum erro** ocorrer no bloco `begin`.
- **`ensure`**: (Opcional) Executado **sempre**, independentemente de erro ou não.

---

##  **Exemplo Básico de Tratamento de Exceção**

### Exemplo 1: Capturando Exceções
```ruby
begin
  puts "Tentando dividir por zero..."
  resultado = 10 / 0
rescue ZeroDivisionError => e
  puts "Erro: #{e.class} - #{e.message}"
end
```

 **Saída:**
```
Tentando dividir por zero...
Erro: ZeroDivisionError - divided by 0
```

### Detalhes:
- Quando o erro `ZeroDivisionError` ocorre, o código dentro de `rescue` é executado.
- O objeto `e` contém informações sobre o erro, como `e.class` (tipo de erro) e `e.message` (mensagem do erro).

---

##  **Capturando Múltiplos Tipos de Erros**
Você pode capturar diferentes tipos de erros em um único bloco `rescue`:

### Exemplo 2: Capturando múltiplos erros
```ruby
begin
  puts "Tentando acessar um arquivo..."
  file = File.open("arquivo_inexistente.txt")
rescue ZeroDivisionError => e
  puts "Erro de divisão: #{e.message}"
rescue IOError => e
  puts "Erro de arquivo: #{e.message}"
end
```

 **Saída:**  
```
Erro de arquivo: No such file or directory @ rb_sysopen - arquivo_inexistente.txt
```

### Detalhes:
- O bloco `rescue` pode ser usado para capturar múltiplos tipos de erros, cada um com seu próprio tratamento.
- **`ZeroDivisionError`** e **`IOError`** são exemplos de diferentes tipos de exceções que podemos capturar e tratar separadamente.

---

##  **Bloco `else`**
O bloco `else` é executado apenas **se nenhum erro ocorrer** no bloco `begin`.

### Exemplo 3: Usando `else`
```ruby
begin
  puts "Tentando realizar uma operação..."
  resultado = 10 / 2
rescue ZeroDivisionError => e
  puts "Erro: #{e.message}"
else
  puts "Operação bem-sucedida! Resultado: #{resultado}"
end
```

 **Saída:**
```
Tentando realizar uma operação...
Operação bem-sucedida! Resultado: 5
```

### Detalhes:
- Se o código dentro de `begin` não gerar erro, o bloco `else` é executado.

---

##  **Bloco `ensure`**
O bloco `ensure` é executado **sempre**, independentemente de erro ou não. Isso é útil quando você precisa garantir que um certo código seja executado, como o fechamento de arquivos ou a liberação de recursos.

### Exemplo 4: Usando `ensure`
```ruby
begin
  puts "Abrindo arquivo..."
  file = File.open("arquivo.txt", "w")
  file.puts "Escrevendo no arquivo"
rescue IOError => e
  puts "Erro de arquivo: #{e.message}"
ensure
  puts "Fechando arquivo..."
  file.close if file
end
```

 **Saída:**
```
Abrindo arquivo...
Fechando arquivo...
```

### Detalhes:
- O código dentro de `ensure` sempre será executado, mesmo que ocorra um erro no bloco `begin`.

---

##  **Levantando Exceções Manualmente**
Em Ruby, você também pode **levantar exceções manualmente** usando a palavra-chave `raise`.

### Exemplo 5: Levantando uma Exceção
```ruby
def dividir(a, b)
  raise "Divisão por zero não permitida" if b == 0
  a / b
end

begin
  puts dividir(10, 0)
rescue => e
  puts "Erro: #{e.message}"
end
```

 **Saída:**
```
Erro: Divisão por zero não permitida
```

### Detalhes:
- A função `dividir` lança uma exceção com a mensagem "Divisão por zero não permitida" se o divisor for zero.

---

##  **Exceções Personalizadas**
Você também pode **criar suas próprias exceções** definindo novas classes de erro.

### Exemplo 6: Exceções Personalizadas
```ruby
class MeuErro < StandardError; end

def fazer_algo
  raise MeuErro, "Algo deu errado!"
end

begin
  fazer_algo
rescue MeuErro => e
  puts "Erro personalizado: #{e.message}"
end
```

 **Saída:**
```
Erro personalizado: Algo deu errado!
```

### Detalhes:
- Criamos uma classe de erro personalizada (`MeuErro`) que herda de `StandardError`.
- Agora podemos lançar e capturar exceções desse tipo em nosso código.

---

##  **Resumo e Boas Práticas**
- **Use `begin` e `rescue`** para capturar exceções e garantir que seu programa não quebre com erros inesperados.
- **Evite capturar erros genéricos** como `rescue => e`, a menos que seja realmente necessário. Prefira capturar erros específicos.
- **Use `ensure`** para garantir que recursos (como arquivos ou conexões) sejam sempre fechados, independentemente de erros.
- **Levante exceções** quando você precisar sinalizar que algo deu errado no seu código, especialmente em métodos.

---

##  **Exercício**
Agora é sua vez! 💪

1️⃣ Crie um método que recebe um número e tenta dividi-lo por outro número. Se o divisor for 0, levante uma exceção personalizada informando que a divisão por zero não é permitida.  
2️⃣ Escreva um programa que tenta abrir um arquivo e, caso o arquivo não exista, mostre uma mensagem de erro. Certifique-se de sempre fechar o arquivo no bloco `ensure`.

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula em construção!!! - Classes e Objetos (POO em Ruby)**