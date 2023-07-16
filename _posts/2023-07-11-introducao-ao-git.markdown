---
layout: post
title:  "Introdução ao git e ao versionamento de código"
date:   2023-07-11 10:00:00 -0300
categories: git versionamento github bitbucket gitlab git-stash
---

![git-versionamento-de-arquivos]({{ site.url }}/assets/git.png){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre uma ferramenta muito bacana para versionar nossos códigos e que já me salvou de vários problemas. Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

Vamos começar com uma visão geral do __Git__ e, em seguida, abordaremos os conceitos de __branches__ e o __fluxo de funcionamento__ do __Git__.

## O que é o Git?
O __Git__ é um __sistema de controle de versão distribuído__ amplamente utilizado no desenvolvimento de software. Ele permite que você controle e acompanhe as alterações feitas nos arquivos de um projeto ao longo do tempo. Com o Git, você pode trabalhar em equipe, colaborar em projetos e manter um histórico completo de todas as modificações feitas em seu código.

## Branches no Git:
No Git, um branch é uma ramificação independente do fluxo principal de desenvolvimento. Ele permite que você trabalhe em diferentes versões do código simultaneamente, sem interferir no trabalho de outras pessoas ou comprometer o código principal do projeto. Cada branch possui seu próprio conjunto de commits, que são as alterações registradas no repositório.

Por exemplo, ao iniciar um projeto, você normalmente tem um branch principal chamado "master" ou "main", que contém a versão estável do código. Ao criar um novo recurso ou correção de bug, você pode criar um novo branch a partir do branch principal. Esse novo branch conterá uma cópia do código no momento em que foi criado e você poderá fazer alterações nesse branch sem afetar o código do branch principal.

## Fluxo de funcionamento do Git:
O Git opera com um fluxo de trabalho baseado em commits. Aqui está uma visão geral do fluxo de funcionamento do Git:

1.  Inicializar um repositório: Primeiro, você inicializa um repositório Git em seu projeto. Isso é feito com o comando __git init__ no diretório raiz do projeto. Após a inicialização, o Git começa a acompanhar as alterações nos arquivos desse diretório.

2.  Adicionar e fazer commits: Você adiciona os arquivos ao Git usando o comando __git add__. Isso indica ao Git que você deseja acompanhar as alterações nesses arquivos. Em seguida, você faz um commit usando o comando __git commit__. Um commit é uma confirmação das alterações feitas nos arquivos, com uma mensagem descritiva que explica as mudanças.

3.  Trabalhar com branches: Para criar um novo branch, você usa o comando __git branch nome-do-branch__. Para mudar para um branch existente, você usa o comando __git checkout nome-do-branch__. Ao alternar para um novo branch, você pode fazer alterações específicas nesse branch sem afetar o código de outros branches.

4.  Mesclar branches: Quando você deseja incorporar as alterações de um branch em outro, você pode realizar uma mesclagem (merge). O Git oferece o comando __git merge__ para fazer isso. A mesclagem combina as alterações feitas em um branch com as alterações do branch atual.

5.  Resolver conflitos: Às vezes, durante uma mesclagem ou ao fazer um pull de alterações de um repositório remoto, podem ocorrer conflitos. Conflitos acontecem quando o Git não consegue determinar automaticamente como combinar as alterações. Nesses casos, você precisa resolver manualmente os conflitos nos arquivos afetados, escolhendo quais alterações manter.

6.  Trabalho com repositórios remotos: O Git permite que você trabalhe com repositórios remotos, como hospedados no GitHub ou GitLab. Você pode adicionar um repositório remoto com o comando __git remote add nome-remoto URL-do-repositório__. Isso permite que você compartilhe seu código com outros desenvolvedores e sincronize seu repositório local com o repositório remoto usando comandos como __git push__ (enviar alterações para o repositório remoto) e __git pull__ (obter alterações do repositório remoto).

Essa é uma visão geral do funcionamento do Git, abordando os conceitos de repositório, branches, commits e mesclagens. O Git oferece uma ampla gama de recursos e comandos para ajudá-lo a controlar e gerenciar seu código de forma eficiente. É __recomendado explorar__ a __documentação do Git__ e tutoriais adicionais para obter uma compreensão mais aprofundada das suas funcionalidades.

Se quise aprender um pouco mais de uma olhada nesse novo [link para o artigo]({% post_url 2023-07-12-como-usar-o-git-comandos-basicos %}) no blog referente aos comandos básicos do git para iniciantes.