---
layout: post
title:  "Instalando docker compose"
date:   2024-12-18 00:00:01 -0300
categories: docker programação desenvolvimento software docker-compose container containers
---

![Docker]({{ site.url }}/assets/docker.jpg){:style="width: 100%" }

Fala pessoal, blz? Se você trabalha com containers Docker, já deve ter percebido que gerenciar múltiplos contêineres pode se tornar uma tarefa complexa. É aqui que entra o Docker Compose, uma ferramenta poderosa que simplifica a orquestração de contêineres. Com ele, você pode definir e executar aplicativos multicontêiner usando um simples arquivo YAML, eliminando a necessidade de gerenciar cada contêiner manualmente.

Neste post, vou mostrar como instalar o Docker Compose no Linux, mais especificamente no Linux Mint (mas o processo também funciona em outras distribuições baseadas no Ubuntu). Vamos detalhar o passo a passo, garantindo que você configure tudo corretamente e possa aproveitar o máximo dessa ferramenta essencial para desenvolvedores e profissionais de infraestrutura.

Para instalar o Docker Compose no **Linux Mint**, você pode seguir os passos abaixo. O processo é similar ao de outras distribuições baseadas no Ubuntu, como o próprio Ubuntu e Debian.

### **Passo 1: Instalar o Docker**
Se você ainda não tem o Docker instalado no Linux Mint, faça isso antes de instalar o Docker Compose.

Caso você ainda não tenha o docker instalado recomendo que veja esse post [Instalando e configurando o docker]({%  link _posts/2023-07-16-instalando-e-configurando-o-docker.markdown %}) antes de seguir o tutorial. Caso você já tenha o docker instalado no seu sistema Linux pode dar sequência no passo a passo.

### **Passo 2: Instalar o Docker Compose**

Existem duas maneiras principais de instalar o Docker Compose no Linux Mint: usando o **Gerenciador de Pacotes (`apt`)** ou baixando o binário oficial.

#### **Método 1: Usando o Gerenciador de Pacotes (mais simples)**

1. Instale o Docker Compose diretamente do repositório:
   ```bash
   sudo apt update
   sudo apt install docker-compose -y
   ```

2. Verifique a instalação:
   ```bash
   docker compose --version
   ```

   > Esse método instala uma versão estável, mas pode não ser a mais recente. Se precisar da última versão, use o método 2.



#### **Método 2: Instalando a Última Versão do Binário Oficial**

1. **Baixe a versão mais recente do Docker Compose:**
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2. **Dê permissão de execução ao binário:**
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. **Verifique a instalação:**
   ```bash
   docker compose --version
   ```

   > Esse método garante que você tenha sempre a versão mais recente do Docker Compose.



### **Passo 3: Testar o Docker Compose**

1. **Crie um arquivo `docker-compose.yml` de exemplo:**
   ```yaml
   version: '3.8'
   services:
     web:
       image: nginx
       ports:
         - "8080:80"
   ```

   Salve esse conteúdo em um arquivo chamado `docker-compose.yml`.

2. **Inicie o Docker Compose:**
   ```bash
   docker compose up -d
   ```

3. **Acesse o serviço:**
   - Abra o navegador e acesse [http://localhost:8080](http://localhost:8080). Você verá a página padrão do **Nginx**.

4. **Encerrar o serviço:**
   ```bash
   docker compose down
   ```



### **Passo 4: Manter o Docker Compose Atualizado**
Se você instalou o Docker Compose via binário oficial (método 2), atualize-o manualmente ao sair novas versões. Basta repetir os comandos de download com o link da nova versão.


Eu te recomendaria seguir o passo 1 pois é o método mais simples de instalar o docker compose!

Caso você prefira tem esse passo a passo no YouTube: [Como Instalar e Configurar Docker Compose no Linux | Guia Completo](https://youtu.be/Rq5YPPytqpw?si=sVvdpwLwIVhFqTpg){:target="_blank"}. Aproveite para nos seguir lá, curtir o vídeo, se inscrever no canal e compartilhar o vídeo com seus amigos!
<iframe width="560" height="315" src="https://www.youtube.com/embed/Rq5YPPytqpw?si=sVvdpwLwIVhFqTpg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>