---
layout: post
title:  "Instalando e configurando a linguagem ruby"
date:   2024-12-15 00:00:01 -0300
categories: ruby rvm linguagem programação desenvolvimento software
---

![Ruby]({{ site.url }}/assets/ruby.png){:style="width: 100%" }

Fala pessoal, blz? O Ruby é uma linguagem de programação poderosa e flexível, amplamente utilizada no desenvolvimento de aplicações web, especialmente com o framework Ruby on Rails. Para gerenciar diferentes versões do Ruby de forma eficiente, o **RVM (Ruby Version Manager)** é uma das ferramentas mais populares entre desenvolvedores.  

Neste guia, você aprenderá como instalar e configurar o Ruby no Linux utilizando o RVM, de maneira simples e prática. Seja você um iniciante ou um desenvolvedor experiente, este passo a passo detalhado vai te ajudar a evitar problemas comuns e deixar o ambiente pronto para seus projetos em Ruby.  

Vamos começar?  

### **1. Atualize seu sistema**
Certifique-se de que seu sistema está atualizado antes de começar:  
```bash
sudo apt update && sudo apt upgrade -y
```

---

### **2. Instale dependências necessárias**
RVM e Ruby precisam de algumas dependências para funcionar corretamente:  
```bash
sudo apt install curl gpg gcc make -y
```

---

### **3. Instale o RVM**
Execute os comandos abaixo para instalar o RVM e adicionar suporte ao Ruby:  

1. **Importe a chave pública do RVM:**  
   ```bash
   gpg --default-keyserver hkps://keys.openpgp.org --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
   ```
   Caso tenha problemas, tente este comando alternativo:  
   ```bash
   gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
   ```

2. **Baixe e instale o RVM:**  
   ```bash
   \curl -sSL https://get.rvm.io | bash -s stable
   ```

Nessa etapa caso você tenha um erro similar a:

```bash
gpg: Can't check signature: No public key
GPG signature verification failed for 
```

Faça:

Esse erro ocorre porque o RVM utiliza assinaturas GPG para validar os arquivos baixados e a chave pública necessária para verificar a assinatura não está disponível no seu sistema. Para corrigir o problema, siga os passos abaixo:

#### ** Baixe as chaves públicas manualmente:**
Execute os seguintes comandos para importar as chaves necessárias:  

- **Chave principal do RVM:**
   ```bash
   gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
   ```

- **Chave adicional do RVM:**
   ```bash
   gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
   ```

Se os comandos acima falharem, você pode importar as chaves diretamente dos servidores do RVM:  

- Importar a chave **mpapis**:
  ```bash
  curl -sSL https://rvm.io/mpapis.asc | gpg --import -
  ```

- Importar a chave **pkuczynski**:
  ```bash
  curl -sSL https://rvm.io/pkuczynski.asc | gpg --import -
  ```

- **Carregue o RVM no shell atual:**  
   ```bash
   source ~/.rvm/scripts/rvm
   ```

---

### **4. Carregue o RVM no shell atual:**  
   ```bash
   source ~/.rvm/scripts/rvm
   ```

### **5. Instale uma versão específica do Ruby**
Agora você pode instalar qualquer versão do Ruby. Por exemplo, para instalar a versão mais recente:  
```bash
rvm install ruby
```

Se você quiser instalar uma versão específica, use:  
```bash
rvm install 3.3.6
```

---

### **6. Configure a versão padrão do Ruby**
Para definir a versão do Ruby que será usada por padrão, execute:  
```bash
rvm use 3.3.6 --default
```

---

### **7. Verifique a instalação**
Confirme se o Ruby foi instalado corretamente:  
```bash
ruby -v
```

### **8. Abrir um terminal interativo com Ruby**
Para abrir um terminal interativo e testar e aprender Ruby execute o seguinte comando no terminal:  
```bash
irb
```
O resultado depois de executar o comando acima será algo assim:

```bash
3.3.6 :001 
```

Aqui para testar o ruby você pode executar o commando puts que permite imprimir alguma informação na sua tela:
```bash
3.3.6 :001 > puts "Hello World!"
Hello World!
 => nil 
3.3.6 :002 > 
```

No caso de desejar executar algum script via terminal basta realizar o seguinte comando trocando o nome meu_script.rb pelo seu script:

```bash
ruby meu_script.rb
```
após executar o comando acima o resultado do seu script deve aparecer no terminal caso você tenha algum comando que imprima algo na tela.

---

### **Dicas extras: **

#### __Atualize o RVM:__
Certifique-se de manter o RVM atualizado para evitar problemas no futuro:  
```bash
rvm get stable
```

#### __Habilitar RVM e o Ruby sempre que abrir o terminal em qualquer diretório:__

Abra o terminal e usando o comando de super usuário __sudo__ use o seu editor de texto favorito nesse caso eu estou usando __nano__

```bash
sudo nano ~/.bashrc
```
Com o nano aberto vá até o final do arquivo aberto nele e adicione o comando a baixo.
```bash
[[ -s "$HOME/.rvm/scripts/rvm"]] && source "$HOME/.rvm/scripts/rvm"
```

após salvar a alteração e sair do nano feche o terminal e abra novamente e verifique se o ruby será encontrado rodando o comando a seguir:
```bash
ruby -v
```

após executar esse comando a versão instalada na sua máquina deverá ser exibida no terminal. Agora você já pode começar a estudar e utilizar ruby na sua jornada de pessoa desenvolvedora Ruby.

Para testar o Ruby no terminal iterativo você pode abrir seu terminal e digitar o comando:

```bash
irb
```
Após executar o comando acima você estará pronto para rodar seus comandos Ruby direto do terminal.