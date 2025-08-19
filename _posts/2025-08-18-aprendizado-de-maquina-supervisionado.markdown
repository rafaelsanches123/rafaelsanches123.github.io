--- 
layout: post
title:  "O que é Aprendizado de Máquina Supervisionado?"
date:   2025-08-18 09:00:00 -0300
categories: aprendizado-de-maquina machine-learning ml aprendizado-de-maquina-supervisionado
---

![Aprendizado-De-Maquina-Supervisionado]({{ site.url }}/assets/aprendizado-supervisionado.png){:style="width: 100%" }

# 📌 O que é Aprendizado de Máquina Supervisionado?

O **aprendizado de máquina supervisionado** é um dos tipos mais utilizados de **Machine Learning**. Nesse paradigma, fornecemos ao algoritmo um **conjunto de dados de entrada** junto com as **respostas corretas (rótulos)**, permitindo que o modelo aprenda a **mapear entradas para saídas**.

👉 Em outras palavras: mostramos exemplos e a resposta certa, e o algoritmo aprende a generalizar para novos casos.


## 🔍 Exemplos práticos

* **Previsão de preços de imóveis**: entrada = tamanho, localização, número de quartos → saída = valor estimado.
* **Classificação de e-mails**: entrada = conteúdo do e-mail → saída = spam ou não spam.
* **Diagnóstico médico**: entrada = exames → saída = diagnóstico provável.


## ⚙️ Principais algoritmos de aprendizado supervisionado

1. **Regressão Linear** – usada para prever valores numéricos (ex: preço de casas).
2. **Regressão Logística** – usada para classificação binária (ex: doença “sim” ou “não”).
3. **Árvores de Decisão** – criam regras baseadas em características dos dados.
4. **Random Forest** – conjunto de várias árvores para melhorar precisão.
5. **Support Vector Machines (SVM)** – encontram fronteiras de decisão entre classes.
6. **K-Nearest Neighbors (KNN)** – classifica novos pontos com base nos vizinhos mais próximos.
7. **Redes Neurais Artificiais** – usadas para problemas mais complexos, como reconhecimento de imagens.

## 🧠 Exemplo simples

Imagine que queremos prever se uma pessoa vai aprovar um **empréstimo bancário**.

* **Entradas**: idade, renda mensal, histórico de crédito.
* **Saída**: aprovado (1) ou não aprovado (0).

Fornecemos ao algoritmo um **conjunto de exemplos já classificados** (pessoas que pediram empréstimo no passado e o resultado). Com base nesses dados, o modelo aprende os padrões e pode prever a aprovação para novos clientes.

## 🚀 Conclusão

O **aprendizado supervisionado** é a base de muitos sistemas que usamos no dia a dia, como filtros de spam, recomendações e diagnósticos automáticos. Ele mostra como **dados rotulados** podem ensinar máquinas a **tomar decisões inteligentes**.

Veja o próximo post dessa série: [Aprendizado de Máquina Não Supervisionado]({% link _posts/2025-08-18-aprendizado-de-maquina-nao-supervisionado.markdown %})
