---
layout: post
title:  "Curso de Ruby - Estruturas de Dados"
date:   2025-03-16 14:10:02 -0300
categories: ruby
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

Arrays e Hashes são duas das estruturas de dados mais fundamentais e utilizadas em Ruby. Vamos explorar cada uma delas e seus métodos mais comuns.

## Arrays

Um **Array** em Ruby é uma coleção ordenada de itens. Esses itens podem ser de qualquer tipo (números, strings, outros arrays, objetos, etc.) e não precisam ser do mesmo tipo dentro do mesmo array. Os arrays são indexados por números inteiros, começando do índice 0 para o primeiro elemento.

**Como criar um Array:**

Existem várias maneiras de criar um array em Ruby:

* **Literal:** Usando colchetes "[ ]" e separando os elementos por vírgula ",".
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    numeros = [1, 2, 3, 4, 5]
    misturado = [1, "dois", 3.0, true]
    vazio = []
    ```

* **Usando `Array.new`:**
    ```ruby
    novo_array = Array.new  # Cria um array vazio
    array_com_tamanho = Array.new(5) # Cria um array com 5 elementos, todos nil
    array_com_tamanho_e_valor_padrao = Array.new(3, "padrão") # Cria um array com 3 elementos, todos "padrão"
    ```

**Métodos Comuns para Manipular Arrays:**

Aqui estão alguns dos métodos mais frequentemente usados para trabalhar com arrays:

**Adicionar Elementos:**

* `push(elemento)` ou `<< elemento`: Adiciona um elemento ao final do array.
    ```ruby
    cores = ["vermelho", "azul"]
    cores.push("verde") # cores agora é ["vermelho", "azul", "verde"]
    cores << "amarelo"  # cores agora é ["vermelho", "azul", "verde", "amarelo"]
    ```

* `unshift(elemento)`: Adiciona um elemento no início do array.
    ```ruby
    cores = ["azul", "verde"]
    cores.unshift("vermelho") # cores agora é ["vermelho", "azul", "verde"]
    ```

* `insert(indice, elemento)`: Insere um elemento em um índice específico.
    ```ruby
    cores = ["vermelho", "verde"]
    cores.insert(1, "azul") # cores agora é ["vermelho", "azul", "verde"]
    ```

**Remover Elementos:**

* `pop`: Remove e retorna o último elemento do array.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    ultimo_elemento = cores.pop # ultimo_elemento é "verde", cores agora é ["vermelho", "azul"]
    ```

* `shift`: Remove e retorna o primeiro elemento do array.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    primeiro_elemento = cores.shift # primeiro_elemento é "vermelho", cores agora é ["azul", "verde"]
    ```

* `delete_at(indice)`: Remove o elemento no índice especificado.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    cores.delete_at(1) # cores agora é ["vermelho", "verde"]
    ```

* `delete(elemento)`: Remove todas as ocorrências do elemento especificado.
    ```ruby
    cores = ["vermelho", "azul", "vermelho", "verde"]
    cores.delete("vermelho") # cores agora é ["azul", "verde"]
    ```

**Acessar Elementos:**

* `[indice]`: Acessa o elemento no índice especificado.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    primeira_cor = cores[0] # primeira_cor é "vermelho"
    segunda_cor = cores[1] # segunda_cor é "azul"
    ultima_cor = cores[-1] # ultima_cor é "verde" (índices negativos contam a partir do final)
    ```

* `first`: Retorna o primeiro elemento do array.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    primeira_cor = cores.first # primeira_cor é "vermelho"
    ```

* `last`: Retorna o último elemento do array.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    ultima_cor = cores.last # ultima_cor é "verde"
    ```

**Iterar sobre Elementos:**

* `each { |elemento| ... }`: Itera sobre cada elemento do array, executando o bloco de código para cada um.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    cores.each { |cor| puts "Eu gosto de #{cor}" }
    ```

* `map { |elemento| ... }`: Itera sobre cada elemento e retorna um novo array com os resultados do bloco.
    ```ruby
    numeros = [1, 2, 3]
    dobro = numeros.map { |numero| numero * 2 } # dobro é [2, 4, 6]
    ```

* `select { |elemento| ... }`: Retorna um novo array contendo apenas os elementos para os quais o bloco retorna `true`.
    ```ruby
    numeros = [1, 2, 3, 4, 5]
    pares = numeros.select { |numero| numero.even? } # pares é [2, 4]
    ```

* `reject { |elemento| ... }`: Retorna um novo array contendo apenas os elementos para os quais o bloco retorna `false`.
    ```ruby
    numeros = [1, 2, 3, 4, 5]
    impares = numeros.reject { |numero| numero.even? } # impares é [1, 3, 5]
    ```

**Informações sobre o Array:**

* `length` ou `size`: Retorna o número de elementos no array.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    tamanho = cores.length # tamanho é 3
    ```

* `empty?`: Retorna `true` se o array estiver vazio, `false` caso contrário.
    ```ruby
    cores =
    vazio = cores.empty? # vazio é true
    ```

* `include?(elemento)`: Retorna `true` se o array contiver o elemento especificado, `false` caso contrário.
    ```ruby
    cores = ["vermelho", "azul", "verde"]
    tem_azul = cores.include?("azul") # tem_azul é true
    tem_amarelo = cores.include?("amarelo") # tem_amarelo é false
    ```

**Transformar o Array:**

* `reverse`: Retorna um novo array com os elementos na ordem inversa.
    ```ruby
    numeros = [1, 2, 3]
    invertido = numeros.reverse # invertido é [3, 2, 1]
    ```

* `sort`: Retorna um novo array com os elementos ordenados.
    ```ruby
    numeros = [3, 1, 4, 1, 5, 9]
    ordenado = numeros.sort # ordenado é [1, 1, 3, 4, 5, 9]
    ```

## Hashes

Um **Hash** em Ruby (também conhecido como dicionário ou mapa em outras linguagens) é uma coleção de pares chave-valor. Cada chave em um hash é única e é usada para acessar o valor correspondente. As chaves podem ser de quase qualquer tipo (strings, símbolos, números, etc.), embora símbolos (`:chave`) e strings (`"chave"`) sejam os mais comuns. Os valores podem ser de qualquer tipo. Ao contrário dos arrays, os hashes não mantêm uma ordem específica dos seus elementos (embora a partir do Ruby 1.9, a ordem de inserção é preservada).

**Como criar um Hash:**

* **Literal:** Usando chaves `{}` e separando os pares chave-valor por vírgula. A chave e o valor são separados por `=>`.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30, "cidade" => "São Paulo" }
    produto = { :nome => "Laptop", :preco => 1200.00 }
    ```

* **Usando `Hash.new`:**
    ```ruby
    novo_hash = Hash.new # Cria um hash vazio
    hash_com_valor_padrao = Hash.new(0) # Cria um hash onde acessar uma chave inexistente retorna 0
    ```

**Métodos Comuns para Manipular Hashes:**

**Adicionar e Atualizar Elementos:**

* `[chave] = valor`: Atribui um valor a uma chave. Se a chave já existir, o valor é atualizado.
    ```ruby
    pessoa = { "nome" => "João" }
    pessoa["idade"] = 30 # Adiciona um novo par chave-valor
    pessoa["nome"] = "Maria" # Atualiza o valor da chave "nome"
    ```

* `store(chave, valor)`: Similar a `= valor`.
    ```ruby
    pessoa = {}
    pessoa.store("nome", "Carlos")
    ```

**Remover Elementos:**

* `delete(chave)`: Remove o par chave-valor com a chave especificada e retorna o valor removido (ou `nil` se a chave não existir).
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    idade_removida = pessoa.delete("idade") # idade_removida é 30, pessoa agora é {"nome"=>"João"}
    ```

* `clear`: Remove todos os pares chave-valor do hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    pessoa.clear # pessoa agora é {}
    ```

**Acessar Elementos:**

* `[chave]`: Retorna o valor associado à chave especificada. Se a chave não existir, retorna `nil` (a menos que um valor padrão tenha sido definido com `Hash.new`).
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    nome = pessoa["nome"] # nome é "João"
    profissao = pessoa["profissao"] # profissao é nil
    ```

* `Workspace(chave)`: Retorna o valor associado à chave especificada. Se a chave não existir, levanta uma exceção `KeyError`. Você também pode fornecer um segundo argumento para `Workspace` como um valor padrão a ser retornado se a chave não for encontrada.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    nome = pessoa.fetch("nome") # nome é "João"
    # profissao = pessoa.fetch("profissao") # Levanta um KeyError
    profissao = pessoa.fetch("profissao", "Não especificado") # profissao é "Não especificado"
    ```

* `values_at(chave1, chave2, ...)`: Retorna um array contendo os valores associados às chaves especificadas.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30, "cidade" => "São Paulo" }
    info = pessoa.values_at("nome", "cidade") # info é ["João", "São Paulo"]
    ```

**Iterar sobre Elementos:**

* `each { |chave, valor| ... }`: Itera sobre cada par chave-valor do hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    pessoa.each { |chave, valor| puts "#{chave}: #{valor}" }
    ```

* `each_key { |chave| ... }`: Itera sobre todas as chaves do hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    pessoa.each_key { |chave| puts "Chave: #{chave}" }
    ```

* `each_value { |valor| ... }`: Itera sobre todos os valores do hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    pessoa.each_value { |valor| puts "Valor: #{valor}" }
    ```

* `map { |chave, valor| ... }`: Itera sobre cada par chave-valor e retorna um novo array com os resultados do bloco.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    detalhes = pessoa.map { |chave, valor| "#{chave} é #{valor}" }
    # detalhes é ["nome é João", "idade é 30"]
    ```

**Informações sobre o Hash:**

* `length` ou `size`: Retorna o número de pares chave-valor no hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    tamanho = pessoa.length # tamanho é 2
    ```

* `empty?`: Retorna `true` se o hash estiver vazio, `false` caso contrário.
    ```ruby
    pessoa = {}
    vazio = pessoa.empty? # vazio é true
    ```

* `key?(chave)` ou `has_key?(chave)` ou `include?(chave)`: Retorna `true` se o hash contiver a chave especificada, `false` caso contrário.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    tem_nome = pessoa.key?("nome") # tem_nome é true
    tem_profissao = pessoa.key?("profissao") # tem_profissao é false
    ```

* `value?(valor)` ou `has_value?(valor)`: Retorna `true` se o hash contiver o valor especificado, `false` caso contrário.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    tem_idade_30 = pessoa.value?(30) # tem_idade_30 é true
    tem_idade_25 = pessoa.value?(25) # tem_idade_25 é false
    ```

**Obter Chaves e Valores:**

* `keys`: Retorna um novo array contendo todas as chaves do hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    chaves = pessoa.keys # chaves é ["nome", "idade"]
    ```

* `values`: Retorna um novo array contendo todos os valores do hash.
    ```ruby
    pessoa = { "nome" => "João", "idade" => 30 }
    valores = pessoa.values # valores é ["João", 30]
    ```

## Exercícios para Praticar
Agora é sua vez! 💪  

Aqui estão alguns exercícios para você praticar a manipulação de Arrays e Hashes em Ruby:

**Exercícios com Arrays:**

1.  Crie um array chamado `frutas` com os seguintes elementos: "maçã", "banana", "laranja".
2.  Adicione a fruta "uva" ao final do array `frutas`.
3.  Adicione a fruta "morango" no início do array `frutas`.
4.  Acesse e imprima o terceiro elemento do array `frutas`.
5.  Remova a fruta "banana" do array `frutas`.
6.  Crie um array chamado `numeros` com os números de 1 a 5. Use o método `map` para criar um novo array contendo o quadrado de cada número.
7.  Dado o array `numeros` (1 a 5), use o método `select` para criar um novo array contendo apenas os números pares.
8.  Verifique se a fruta "manga" está presente no array `frutas`. Imprima o resultado (true ou false).

**Exercícios com Hashes:**

9.  Crie um hash chamado `aluno` com as seguintes chaves e valores: `:nome` => "Maria", `:matricula` => 12345, `:curso` => "Engenharia".
10. Adicione um novo par chave-valor ao hash `aluno`: `:nota` => 8.5.
11. Acesse e imprima o nome do aluno a partir do hash `aluno`.
12. Remova a chave `:matricula` do hash `aluno`.
13. Crie um array de hashes chamado `livros`. Cada hash deve representar um livro com as chaves `:titulo` e `:autor`. Adicione pelo menos dois livros ao array.
14. Itere sobre o array `livros` e imprima o título de cada livro.
15. Crie um hash chamado `contagem_cores` para contar a ocorrência de cores em um array (ex: `["vermelho", "azul", "vermelho", "verde"]`). Itere sobre o array de cores e atualize a contagem no hash.
16. Dado o hash `aluno`, verifique se a chave `:nota` existe. Imprima o resultado (true ou false).

**Se quiser, tente resolver e envie nos comentários seus códigos e suas respostas para analisarmos juntos!** 🚀

**Próxima aula - [Manipulação de Arquivos]({% link _posts/2025-03-17-curso-de-ruby-manipulacao-de-arquivos.markdown %})**