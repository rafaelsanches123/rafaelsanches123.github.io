---
layout: post
title:  "Curso de Ruby - Manipulação de Arquivos"
date:   2025-03-17 09:45:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

A manipulação de arquivos é uma tarefa comum e importante em qualquer linguagem de programação. Ruby oferece uma maneira simples e poderosa de trabalhar com arquivos, permitindo abrir, ler, escrever e fechar arquivos facilmente.

---

##  **Abrindo Arquivos**

### Abertura de Arquivo com `File.open`

A maneira mais comum de trabalhar com arquivos em Ruby é utilizando o método `File.open`. Ele permite abrir um arquivo em diferentes modos (leitura, escrita, etc.) e realizar operações nele.

A sintaxe básica é:

```ruby
file = File.open("caminho/do/arquivo", "modo")
```

Onde:
- `"caminho/do/arquivo"` é o caminho do arquivo.
- `"modo"` define como você vai interagir com o arquivo (veremos os modos abaixo).

---

##  **Modos de Abertura de Arquivo**

Os principais modos de abertura de arquivos são:

- **`"r"`**: Leitura (leitura simples do arquivo).
- **`"w"`**: Escrita (cria um novo arquivo ou sobrescreve um arquivo existente).
- **`"a"`**: Adição (abre o arquivo para adicionar conteúdo no final).
- **`"r+"`**: Leitura e escrita (abre o arquivo para leitura e escrita).
- **`"w+"`**: Leitura e escrita (cria um novo arquivo ou sobrescreve um existente).

---

### Exemplo 1: Abrindo um Arquivo para Leitura
```ruby
file = File.open("exemplo.txt", "r")
conteudo = file.read
puts conteudo
file.close
```

 **Saída**: O conteúdo do arquivo `exemplo.txt` será impresso no console.

### Detalhes:
- `file.read` lê todo o conteúdo do arquivo.
- `file.close` fecha o arquivo após a operação.

---

### Exemplo 2: Abrindo um Arquivo para Escrita
```ruby
file = File.open("exemplo.txt", "w")
file.puts "Olá, mundo!"
file.close
```

 **Saída**: O arquivo `exemplo.txt` será criado (ou sobrescrito) com o conteúdo "Olá, mundo!".

### Detalhes:
- O método `file.puts` escreve uma linha no arquivo.
- Se o arquivo já existir, ele será **sobrescrito**.

---

### Exemplo 3: Abrindo um Arquivo para Adicionar Conteúdo
```ruby
file = File.open("exemplo.txt", "a")
file.puts "Mais uma linha."
file.close
```

 **Saída**: O conteúdo "Mais uma linha." será adicionado ao final do arquivo `exemplo.txt`.

---

##  **Leitura de Arquivo Linha por Linha**

Se você deseja ler um arquivo linha por linha, pode usar o método `each_line`.

### Exemplo 4: Lendo Linha por Linha
```ruby
file = File.open("exemplo.txt", "r")
file.each_line do |linha|
  puts linha
end
file.close
```

 **Saída**: Cada linha do arquivo será impressa no console.

### Detalhes:
- `each_line` itera sobre cada linha do arquivo, permitindo processar linha por linha.

---

##  **Trabalhando com Arquivos Usando `File.read` e `File.write`**

Em vez de abrir o arquivo explicitamente, você pode usar os métodos de leitura e escrita diretamente.

### Exemplo 5: Usando `File.read` para Ler Todo o Conteúdo
```ruby
conteudo = File.read("exemplo.txt")
puts conteudo
```

 **Saída**: O conteúdo do arquivo será impresso no console.

### Exemplo 6: Usando `File.write` para Escrever no Arquivo
```ruby
File.write("exemplo.txt", "Nova linha no arquivo.")
```

 **Saída**: O arquivo `exemplo.txt` será sobrescrito com o conteúdo "Nova linha no arquivo."

---

##  **Verificando se um Arquivo Existe**

Antes de tentar abrir um arquivo, é importante verificar se ele existe para evitar erros.

### Exemplo 7: Verificando Existência de Arquivo
```ruby
if File.exist?("exemplo.txt")
  puts "O arquivo existe."
else
  puts "O arquivo não existe."
end
```

 **Saída**: Será impresso se o arquivo `exemplo.txt` existe ou não no diretório atual.

### Detalhes:
- O método `File.exist?` retorna `true` se o arquivo existir, caso contrário, retorna `false`.

---

##  **Removendo um Arquivo**

Se você deseja excluir um arquivo, pode usar o método `File.delete`.

### Exemplo 8: Deletando um Arquivo
```ruby
File.delete("exemplo.txt") if File.exist?("exemplo.txt")
```

 **Saída**: O arquivo `exemplo.txt` será removido, se existir.

### Detalhes:
- `File.delete` exclui o arquivo do sistema.
- Verifique sempre se o arquivo existe antes de excluí-lo para evitar erros.

---

##  **Criando Diretórios**

Além de manipular arquivos, você pode criar diretórios usando o método `Dir.mkdir`.

### Exemplo 9: Criando um Diretório
```ruby
Dir.mkdir("novo_diretorio") unless Dir.exist?("novo_diretorio")
```

 **Saída**: Será criado o diretório `novo_diretorio`, caso ele ainda não exista.

### Detalhes:
- `Dir.mkdir` cria um diretório.
- `Dir.exist?` verifica se um diretório já existe.

---

##  **Trabalhando com Arquivos Temporários**

Ruby também permite trabalhar com arquivos temporários de maneira simples. Para isso, usamos a classe `Tempfile`.

### Exemplo 10: Criando e Usando um Arquivo Temporário
```ruby
require 'tempfile'

tempfile = Tempfile.new('exemplo')
tempfile.puts "Este é um arquivo temporário"
tempfile.rewind  # Volta para o início do arquivo
puts tempfile.read  # Lê o conteúdo
tempfile.close  # Fecha o arquivo temporário
tempfile.unlink  # Remove o arquivo temporário
```

 **Saída:**
```
Este é um arquivo temporário
```

### Detalhes:
- `Tempfile.new('prefixo')` cria um arquivo temporário.
- `tempfile.close` e `tempfile.unlink` garantem que o arquivo seja fechado e excluído após o uso.

---

##  **Exercício**
Agora é sua vez! 💪

1️⃣ Crie um programa que leia um arquivo de texto e conte quantas linhas ele possui.  
2️⃣ Crie um programa que abra um arquivo para escrita, adicione 5 linhas nele e depois leia o conteúdo.  
3️⃣ Crie um arquivo temporário, escreva algo nele, leia e imprima seu conteúdo, e depois exclua o arquivo.

---

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula - [Tratamento de Exceções]({% link _posts/2025-03-17-curso-de-ruby-tratamento-de-excecoes.markdown %})**