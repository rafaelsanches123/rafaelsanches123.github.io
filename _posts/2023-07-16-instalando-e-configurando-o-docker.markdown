---
layout: post
title:  "Instalando e configurando o docker"
date:   2023-07-16 18:00:00 -0300
categories: docker
---

![docker]({{ site.url }}/assets/docker.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre uma ferramenta que chegou para ajudar muitos desenvolvedores com aquele famoso problema "Na minha máquina funciona". Vamos descobrir juntos como instalar e configurar essa ferramenta no seu PC/notebook. Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

## Docker

O Docker é uma plataforma que permite criar, implantar e executar aplicativos em contêineres. Os contêineres são unidades isoladas de software que contêm todas as dependências necessárias para executar um aplicativo. Para entender melhor o docker sugiro dar uma lida antes nesse [artigo sobre o Docker]({% post_url 2023-07-16-o-que-e-docker %})

## Instalando e configurando o docker

Aqui está um guia detalhado para instalar e configurar o Docker em sistemas operacionais Windows, macOS e Linux:

### Windows:

1.   Baixe o instalador do Docker para Windows no site oficial (https://www.docker.com/products/docker-desktop).

2.   Execute o instalador baixado e siga as instruções de instalação. Durante a instalação, pode ser necessário ativar a virtualização na BIOS do seu computador, caso ainda não esteja habilitada.

3.   Após a conclusão da instalação, o Docker deve ser iniciado automaticamente. Você pode verificar se o Docker está em execução procurando o ícone do Docker na barra de tarefas do Windows.

### macOS:

1.  Baixe o instalador do Docker para macOS no site oficial (https://www.docker.com/products/docker-desktop).

2.  Execute o instalador baixado e siga as instruções de instalação.

3.  Após a conclusão da instalação, o Docker deve ser iniciado automaticamente. Você pode verificar se o Docker está em execução procurando o ícone do Docker na barra de menus do macOS.

### Linux:

A instalação do Docker no Linux pode variar um pouco dependendo da distribuição específica. Aqui estão os passos gerais para instalar o Docker em sistemas Linux baseados em Debian/Ubuntu:

1.  Abra um terminal.
2.  Atualize o índice de pacotes do sistema:
```bash
    sudo apt update
```
3.  Instale as dependências necessárias para permitir que o sistema use repositórios HTTPS:
```bash
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```
4.  Adicione a chave GPG oficial do Docker ao sistema:
```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
5.  Adicione o repositório do Docker às fontes do APT:
```bash
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
6.  Atualize novamente o índice de pacotes do sistema:
```bash
    sudo apt update
```

    Caso você tenha esse erro:

    ```bash
    Reading package lists... Done
    E: The repository 'https://download.docker.com/linux/ubuntu wilma Release' does not have a Release file.
    N: Updating from such a repository can't be done securely, and is therefore disabled by default.
    N: See apt-secure(8) manpage for repository creation and user configuration details.
    ```

    O erro ocorre porque o codinome da sua versão do Linux Mint (provavelmente `wilma` para o Mint 22) não é oficialmente suportado pelo repositório do Docker. Mas como o Linux Mint é baseado no Ubuntu, você pode usar o codinome correspondente da versão do Ubuntu. O Mint 22 é baseado no **Ubuntu 22.04 (Jammy Jellyfish)**.

    Aqui está como corrigir:

    * **Edite o arquivo de repositório do Docker**
    Abra o arquivo com um editor de texto:
    ```bash
    sudo nano /etc/apt/sources.list.d/docker.list
    ```

    Substitua o `$(lsb_release -cs)` ou `wilma` por `jammy`:
    ```bash
    deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu jammy stable
    ```

    Salve o arquivo e feche o editor (`Ctrl+O`, `Enter`, depois `Ctrl+X` no Nano).

    * **Atualize os pacotes novamente**
    Execute o comando para atualizar a lista de pacotes:
    ```bash
    sudo apt update
    ```

    Caso não tenha o erro acima pode seguir com o passo a passo:

7.  Instale a versão mais recente do Docker:
```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io
```
8.  Inicie e habilite o serviço do Docker:
```bash
    sudo systemctl start docker
    sudo systemctl enable docker
```

### Configuração do Docker (Opcional):

Após instalar o Docker, você pode configurar algumas opções adicionais, como permitir que um usuário não privilegiado execute comandos Docker sem a necessidade de "sudo" (apenas para Linux):

1.  Adicione seu usuário ao grupo "docker":

```bash
    sudo usermod -aG docker $USER
```

2.  Encerre a sessão atual e faça login novamente para que as alterações tenham efeito.

Agora você instalou e configurou o Docker em seu sistema! Você pode testar a instalação executando o comando __docker --version__ no __terminal__ para verificar a versão do Docker instalada. Para começar a usar o Docker, confira a documentação oficial ou tutoriais adicionais para criar, executar e gerenciar contêineres.

Caso você prefira tem esse passo a passo no YouTube: [Instalando e configurando o docker no linux](https://youtu.be/gkK7c_BJdBY?si=tWfUgJfy1eU5In5f){:target="_blank"}. Aproveite para nos seguir lá, curtir o vídeo, se inscrever no canal e compartilhar o vídeo com seus amigos!

<iframe width="560" height="315" src="https://www.youtube.com/embed/gkK7c_BJdBY?si=OZQGxkYgVkKN97kc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>