--- 
layout: post
title:  "O que é Aprendizado de Máquina Não Supervisionado?"
date:   2025-08-18 10:00:00 -0300
categories: aprendizado-de-maquina machine-learning ml aprendizado-de-maquina-nao-supervisionado
---

![Aprendizado-De-Maquina-Nao-Supervisionado]({{ site.url }}/assets/aprendizado-nao-supervisionado.png){:style="width: 100%" }

# 📌 O que é Aprendizado de Máquina Não Supervisionado?

O **aprendizado não supervisionado** é um tipo de **Machine Learning** em que os algoritmos recebem **dados sem rótulos**.
Isso significa que, ao contrário do aprendizado supervisionado, não existe uma resposta correta já conhecida. O objetivo é **descobrir padrões escondidos** e **estruturas naturais** dentro dos dados.

👉 Em resumo: o modelo “explora os dados por conta própria” e encontra relações que não foram explicitamente fornecidas.


## 🔍 Exemplos práticos

* **Segmentação de clientes**: agrupar consumidores com comportamentos de compra semelhantes.
* **Análise de redes sociais**: identificar comunidades ou grupos de interesse.
* **Compressão de dados**: reduzir a dimensionalidade mantendo informações importantes.
* **Detecção de anomalias**: identificar comportamentos incomuns, como fraudes bancárias.


## ⚙️ Principais técnicas de aprendizado não supervisionado

### 1. **Clustering (Agrupamento)**

Algoritmos que dividem os dados em grupos com características semelhantes.

* **K-Means**
* **DBSCAN**
* **Hierarchical Clustering**

### 2. **Redução de Dimensionalidade**

Usada para simplificar dados muito complexos, facilitando a visualização e análise.

* **PCA (Principal Component Analysis)**
* **t-SNE (t-Distributed Stochastic Neighbor Embedding)**
* **Autoencoders**


## 🧠 Exemplo simples

Imagine que uma loja online queira entender melhor seus clientes.

* **Entradas**: histórico de compras, frequência de acesso, valores gastos.
* **Sem saídas definidas** (sem rótulos).

O algoritmo de **clustering** pode agrupar os clientes em **três grupos**:

1. Compradores frequentes e de alto valor.
2. Compradores ocasionais de médio valor.
3. Compradores raros de baixo valor.

Esse resultado pode ser usado para estratégias de **marketing personalizado**.


## 🚀 Conclusão

O **aprendizado não supervisionado** é essencial para **descobrir insights escondidos nos dados**.
Ele é usado em situações onde não temos rótulos, mas queremos identificar **estruturas, padrões ou anomalias**.

Com ele, empresas conseguem entender melhor seus clientes, detectar fraudes e até reduzir a complexidade de grandes volumes de dados.


👉 Esse tipo de aprendizado é um passo além do supervisionado, pois ajuda a **revelar o desconhecido**.

Veja o próximo post dessa série: [Aprendizado de Máquina Por Reforço]({% link _posts/2025-08-18-aprendizado-de-maquina-por-reforco.markdown %})