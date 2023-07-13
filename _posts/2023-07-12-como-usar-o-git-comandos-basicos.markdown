---
layout: post
title:  "Como usar o git e comandos básicos"
date:   2023-07-12 21:50:00 -0300
categories: git versionamento github bitbucket gitlab
---

![git-versionamento-de-arquivos]({{ site.url }}/assets/git.png){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre uma tecnologia super simples e muito poderoza utilizada para __versionar__ nossos arquivos de código na hora de desenvolver qualaquer projeto seja ele pessoal ou não. Quer saber mais? Se a respostar for sim, continue comigo que eu vou te ajudar nisso!

## Git

O __Git__ é um __sistema de controle de versão distribuído__ que permite __rastrear alterações__ e __colaborar__ em projetos com outros desenvolvedores. Ele é comumente usado no desenvolvimento de software, mas também pode ser útil para gerenciar qualquer tipo de projeto que envolva vários colaboradores ou precise de controle de versão. Aqui está um guia passo a passo para ajudá-lo a começar com o Git:

1. Instale o Git:

    * Acesse o site oficial do Git ([https://git-scm.com/](https://git-scm.com/)) e faça o download da versão do Git adequada para o seu sistema operacional.
    * Execute o instalador e siga as instruções para concluir a instalação.
2. Configure sua identidade:

    * Abra um __terminal__ (e.g., Linux ou Mac) ou __prompt de comando__(e.g.,Windows).
    * Configure seu nome e endereço de e-mail executando os seguintes comandos, substituindo os espaços reservados pelo seu nome e e-mail reais:
    ```bash
        git config --global user.name "Seu Nome"
        git config --global user.email "seu@email.com"
    ```
    * Essas informações serão usadas para identificar seus commits.
3.  Crie um novo repositório:

    * Navegue até o diretório onde você deseja inicializar um repositório Git. Isso pode ser um projeto existente ou um novo diretório que você criar.
    * Execute o seguinte comando para criar um novo repositório Git:
    ```bash
        git init
    ```
    * Isso inicializa um repositório Git vazio no diretório atual.

4.  Comece a rastrear arquivos:

    * Adicione os arquivos que você deseja rastrear ao repositório Git. Você pode adicionar arquivos individuais ou diretórios inteiros. Por exemplo, para adicionar um único arquivo, use o comando:
    ```bash
        git add nome_do_arquivo
    ```
    Para adicionar um diretório, use o comando:
    ```bash
        git add nome_do_diretorio/
    ```
    Para adicionar todos os arquivos no diretório atual, use:
    ```bash
        git add .
    ```
5.  Faça um commit:

    * Depois de adicionar os arquivos, você precisa criar um commit para salvar as alterações. Um commit é uma captura instantânea do repositório em um ponto específico no tempo.
    * Execute o seguinte comando para criar um commit:
    ```bash
        git commit -m "Commit inicial"
    ```
    * Substitua "Commit inicial" por uma mensagem descritiva que explique as alterações que você fez.

6.  Trabalhando com repositórios remotos:

    * Se você deseja colaborar com outras pessoas ou fazer backup do seu código em um servidor remoto, pode conectar seu repositório local a um repositório remoto (como um hospedado no GitHub, GitLab ou Bitbucket).
    * Crie um novo repositório no serviço remoto e obtenha sua URL.
    * Execute o seguinte comando para adicionar um repositório remoto:
    ```bash
        git remote add origin <url_do_repositorio_remoto>
    ```
    * Substitua <url_do_repositorio_remoto> pela URL do repositório remoto.

7.  Enviando e recebendo alterações:
    * Para enviar seus commits locais (i.e., etapa 5) para o repositório remoto, use o comando:
    ```bash
        git push origin master
    ```
    * Isso envia suas alterações locais para o branch master do repositório remoto.
    * Para obter as últimas alterações do repositório remoto, use o comando:
    ```bash
        git pull origin master
    ```
    * Isso obtém as alterações do branch master do repositório remoto e mescla-as no seu branch local.
    * Esses são os passos básicos para começar a usar o Git. No entanto, o Git oferece muitos outros recursos e comandos para branchs, mesclagens, resolução de conflitos e colaboração com outros desenvolvedores. Eu incentivo você a explorar a documentação e tutoriais do Git para aprofundar seu conhecimento sobre suas capacidades.