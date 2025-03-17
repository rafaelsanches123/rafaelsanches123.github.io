---
layout: post
title:  "Jogo das Luzes"
date:   2025-03-17 15:15:00 -0300
categories: jogo programação desenvolvimento lógica desafio
---

![JogoDasLuzes]({{ site.url }}/assets/jogo-das-luzes.jpg){:style="width: 100%" }

O jogo das luzes foi um jogo que eu tive o prazer de implementar durante o meu primeiro ano de faculdade enquanto eu aprendia programação e acredito que ele é ótimo e fundamental para estimular a lógica e a criatividade aplicadas na resolução de problemas utilizando o feijão com arroz da programação além de te ajudar a se tornar um programador muito melhor.

Para começar vamos falar sobre a lógica do jogo: 

Você vai precisar imprimir na tela do usuário um menu onde ele vai ter as seguintes opçoes:

1. Jogar
2. Ranking
3. Sair

**Começando pela opção 1 do menu (Jogar)**:

Deverá ser perguntado a pessoa jogadora seu nome ou apelido. Após saber o nome da pessoa jogadora você deverá perguntar a quantidade de tentativas que ela deseja utilizar para vencer o jogo sendo que o valor minimo são 25 tentativas. A pessoa jogadora poderá vencer o jogo em menos tentativas ok.

Após captar a quantidade de jogadas estabelecidas pela pessoa jogadora você deverá imprimir para ela na tela o seguinte cenário:

Imagine um tabuleiro que possui 5 linhas e 5 colunas onde, o cruzamente entre as linhas e colunas representam posições no tabuleiro e o jogo começa com todas as casas com as luzes desligadas. No nosso exemplo vamos representar o tabuleiro por meio de uma matriz onde temos cada uma de suas posições preenchidas com o valor zero "0" para representar que as luzes no tabuleiro seguem desligadas ao iniciar o jogo.

**Exemplo do tabuleiro com as luzes desligadas:**

| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|
|:---:	|:---:	|:---:	|:---:	|:---:	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|

Após o tabuleiro ser apresentado ao usuário em seu estado atual você deverá solicitar a pessoa jogadora que ela informe a linha e a coluna (posição no tabuleiro) da qual ela desejar acender ou desligar uma lampada específica.

No nosso caso quando uma posição for informada e ela estiver desligada representada pelo valor "0" o seu valor será trocado por "1" e aquela posição passará a ser ligada. Fácil não é mesmo? O mecanismo é basicamente similar a um interruptor.

**Detalhe e regra do jogo**: sempre que uma posição for alterada as **posições adjascentes** da **esquerda**, da **direita**, de **cima** e de **baixo** também **devem ser trocadas**. Caso uma luz esteja desligada ela passa a ficar ligada e caso ela esteja ligada ela passa a ficar desligada.

Exemplo: vamos dar início a primeira jogada e vamos escolher a posição **L=2** e **C=2** (equivalente a **linha (L)** 2 e **coluna (C)** 2). Nesse caso após realizar a jogada nosso tabuleiro ficará assim:

| **0** 	| **1** 	| **0** 	| **0** 	| **0** 	|
|:---:	|:---:	|:---:	|:---:	|:---:	|
| **1** 	| **1** 	| **1** 	| **0** 	| **0** 	|
| **0** 	| **1** 	| **0** 	| **0** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|

Agora vamos realizar uma nova jogada escolhendo a posição: **L=2** e **C=4**;

| **0** 	| **1** 	| **0** 	| **1** 	| **0** 	|
|:---:	|:---:	|:---:	|:---:	|:---:	|
| **1** 	| **1** 	| **0** 	| **1** 	| **1** 	|
| **0** 	| **1** 	| **0** 	| **1** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|
| **0** 	| **0** 	| **0** 	| **0** 	| **0** 	|

Como foi possível observar as posições adjascentes da direita, de cima e de baixo estavam desligadas então, passaram a ficar ligadas e a posição adjascente da esquerda estava ligada
logo, passou a ficar desligada como reflete o tabuleiro acima.

Regra: você só pode escolher posições tal que:
**C** > 0 e **C** < 6;
**L** > 0 e **L** < 6;

Outras regras importantes:
* Um nome só entra no ranking quando ele completa o jogo caso o contrário ele não entra;
* O número de jogadas é limitado até 999;
* Caso duas pessoas jogadoras vençam o jogo com a mesma quantidade de jogadas o desempate acontece por meio do tempo gasto para finalizar o jogo e a ordem de desempate segue por meio da hora, minuto e segundo gastos para sua conclusão;
* Lembre-se que a pessoa jogadora pode cometer erros então é importante sempre validar cada jogada e verificar a linha e a coluna da posição desejada se estão condizentes com o tamanho do tabuleiro.

A seguir um exemplo do tabuleiro finalizado:

| **1** 	| **1** 	| **1** 	| **1** 	| **1** 	|
|:---:	|:---:	|:---:	|:---:	|:---:	|
| **1** 	| **1** 	| **1** 	| **1** 	| **1** 	|
| **1** 	| **1** 	| **1** 	| **1** 	| **1** 	|
| **1** 	| **1** 	| **1** 	| **1** 	| **1** 	|
| **1** 	| **1** 	| **1** 	| **1** 	| **1** 	|

Bom, agora que você já entendeu o jogo bora botar pra quebrar e implementar um jogo incrível para ficar fera na linguagem de programação que você está estudando pelo blog nesse exato momento! Não esqueça de compartilhar nos comentários o resultado do seu desafio e inspirar mais pessoas a fazer o mesmo! Detalhe importante você pode implementar da forma que achar melhor desde que use os recurso que foram ensinados durante o seu curso realizado pelos posts no blog. 

**Regra master**: você não deve usar nenhuma biblioteca de terceiros/externa somente recursos nativos.

Caso sinta-se a vontade compartilhe o seu github ou outro repositório onde tenha documentado/armazenado/versionado seu código do jogo implementado! Lembre-se informe nos comentários.

Para te ajudar ainda mais fiz essa ilustração para te inspirar e ajudar no entendimento:

![JogoDasLuzes]({{ site.url }}/assets/jogo-das-luzes-regras.png){:style="width: 100%" }
