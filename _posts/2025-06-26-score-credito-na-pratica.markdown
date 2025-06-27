--- 
layout: post
title:  "Score de Crédito na Prática"
date:   2025-06-26 08:00:00 -0300
categories: score-de-crédito análise-de-dados variáveis-estatísticas book-de-variáveis finanças-pessoais empréstimo inadimplência risco-de-crédito
---

![Imagem-Credfacil]({{ site.url }}/assets/credfacil.png){:style="width: 100%" }

Agora que você já entendeu os fundamentos do score de crédito (como explicamos anteriormente neste post), vamos colocar a mão na massa! Criaremos juntos um cenário fictício para construir um score simplificado e consolidar seus conhecimentos de forma prática.

**Nosso Cenário Fictício: "CrediFácil" - Uma Pequena Fintech de Empréstimos Pessoais**

A "CrediFácil" é uma fintech que oferece pequenos empréstimos pessoais online. Para decidir se aprova ou não um empréstimo e qual taxa de juros aplicar, a empresa precisa avaliar o risco de inadimplência de cada solicitante. Para isso, eles decidiram criar um score de crédito interno.

**1. Identificação das Variáveis Estatísticas Relevantes (Dataset Fake)**

Após analisar dados de clientes anteriores (um dataset fake que criaremos), a CrediFácil identificou algumas variáveis que parecem estar relacionadas à probabilidade de um cliente pagar o empréstimo em dia. Vamos criar um pequeno dataset fake com essas variáveis para alguns solicitantes:

```python
import pandas as pd
import numpy as np

# Definindo um seed para reprodutibilidade
np.random.seed(42)

data = {
    'ID_Cliente': range(1, 21),
    'Idade': np.random.randint(20, 65, 20),
    'Renda_Mensal': np.random.randint(1500, 10000, 20),
    'Tempo_Emprego_Anos': np.random.randint(0, 15, 20),
    'Historico_Credito': np.random.choice(['Bom', 'Regular', 'Ruim'], size=20, p=[0.6, 0.3, 0.1]),
    'Valor_Emprestimo_Solicitado': np.random.randint(500, 5000, 20),
    'Inadimplente': np.random.choice([0, 1], size=20, p=[0.8, 0.2]) # 0 = Não Inadimplente, 1 = Inadimplente
}

df = pd.DataFrame(data)
print(df)
```

**2. Criação do Book de Variáveis da CrediFácil**

Para garantir que todos na CrediFácil entendam as variáveis utilizadas, criamos um book de variáveis simples:

| Nome da Variável           | Descrição                                                                 | Tipo        | Formato   | Valores Possíveis (Exemplos) | Observações                                                                 |
| :------------------------- | :------------------------------------------------------------------------ | :---------- | :-------- | :--------------------------- | :-------------------------------------------------------------------------- |
| `ID_Cliente`              | Identificador único do cliente.                                          | Qualitativa | Numérico  | 1, 2, 3, ...                 | Chave primária.                                                             |
| `Idade`                   | Idade do solicitante em anos.                                            | Quantitativa| Inteiro   | 20, 35, 58, ...              |                                                                             |
| `Renda_Mensal`            | Renda mensal bruta do solicitante em Reais (R$).                           | Quantitativa| Inteiro   | 1800, 5500, 9200, ...        |                                                                             |
| `Tempo_Emprego_Anos`      | Tempo em anos que o solicitante está empregado no seu trabalho atual.     | Quantitativa| Inteiro   | 0, 2, 10, ...                | 0 indica desempregado ou emprego muito recente.                             |
| `Historico_Credito`       | Histórico de crédito do solicitante consultado em birôs de crédito.        | Qualitativa | Nominal   | 'Bom', 'Regular', 'Ruim'     | Reflete o comportamento de pagamento anterior.                               |
| `Valor_Emprestimo_Solicitado` | Valor do empréstimo que o cliente está solicitando em Reais (R$).        | Quantitativa| Inteiro   | 750, 2300, 4800, ...        |                                                                             |
| `Inadimplente`            | Indica se o cliente inadimpliu o empréstimo (1) ou não (0) (para análise). | Qualitativa | Binário   | 0, 1                       | Esta é a nossa variável alvo, que queremos prever com o score.              |

**3. Criação de um Score de Crédito Simplificado**

Para este exemplo, vamos criar um score de crédito bem simples, atribuindo pontos para diferentes faixas de cada variável que consideramos positiva para a capacidade de pagamento:

  * **Idade:**
      * 25 - 45 anos: 2 pontos
      * Outras idades: 0 pontos
  * **Renda Mensal:**
      * Acima de R$ 3000: 3 pontos
      * Entre R$ 2000 e R$ 3000: 1 ponto
      * Abaixo de R$ 2000: 0 pontos
  * **Tempo de Emprego (Anos):**
      * Acima de 2 anos: 2 pontos
      * Até 2 anos: 0 pontos
  * **Histórico de Crédito:**
      * 'Bom': 4 pontos
      * 'Regular': 1 ponto
      * 'Ruim': 0 pontos
  * **Valor do Empréstimo Solicitado (em relação à renda):**
      * Valor do Empréstimo \<= 30% da Renda Mensal: 3 pontos
      * Valor do Empréstimo \> 30% da Renda Mensal: 0 pontos

Vamos calcular o score para cada cliente no nosso dataset fake:

```python
def calcular_score(row):
    score = 0

    # Idade
    if 25 <= row['Idade'] <= 45:
        score += 2

    # Renda Mensal
    if row['Renda_Mensal'] > 3000:
        score += 3
    elif 2000 <= row['Renda_Mensal'] <= 3000:
        score += 1

    # Tempo de Emprego
    if row['Tempo_Emprego_Anos'] > 2:
        score += 2

    # Histórico de Crédito
    if row['Historico_Credito'] == 'Bom':
        score += 4
    elif row['Historico_Credito'] == 'Regular':
        score += 1

    # Valor do Empréstimo vs Renda
    if row['Valor_Emprestimo_Solicitado'] <= 0.3 * row['Renda_Mensal']:
        score += 3

    return score

df['Score_Credito'] = df.apply(calcular_score, axis=1)
print(df[['ID_Cliente', 'Idade', 'Renda_Mensal', 'Tempo_Emprego_Anos', 'Historico_Credito', 'Valor_Emprestimo_Solicitado', 'Score_Credito', 'Inadimplente']])
```

**4. Análise e Tomada de Decisão com o Score**

Agora que temos um score de crédito para cada cliente, a CrediFácil pode definir faixas de score para diferentes níveis de risco e tomar decisões sobre a aprovação do empréstimo e a taxa de juros:

  * **Score Alto (Ex: 9-14 pontos):** Baixo risco de inadimplência. Aprovação de empréstimo quase certa, com taxas de juros mais baixas.
  * **Score Médio (Ex: 5-8 pontos):** Risco moderado de inadimplência. Aprovação pode depender de outras análises ou de um valor de empréstimo menor, com taxas de juros intermediárias.
  * **Score Baixo (Ex: 0-4 pontos):** Alto risco de inadimplência. Empréstimo provavelmente negado ou oferecido com taxas de juros muito altas para compensar o risco.

Vamos analisar nosso dataset fake com base nesse score:

```python
def avaliar_risco(score):
    if score >= 9:
        return 'Baixo Risco'
    elif score >= 5:
        return 'Risco Moderado'
    else:
        return 'Alto Risco'

df['Nivel_Risco'] = df['Score_Credito'].apply(avaliar_risco)
print(df[['ID_Cliente', 'Score_Credito', 'Nivel_Risco', 'Inadimplente']])

# Podemos também analisar a relação entre o score e a inadimplência no nosso dataset fake
print("\nAnálise da relação entre Score e Inadimplência:")
print(df.groupby('Nivel_Risco')['Inadimplente'].mean())
```

**Storytelling e Conclusão**

A CrediFácil implementou um score de crédito simplificado utilizando variáveis estatísticas como idade, renda, tempo de emprego, histórico de crédito e o valor do empréstimo solicitado em relação à renda. O book de variáveis garantiu que todos entendessem o significado de cada variável e como ela seria utilizada no cálculo do score.

O score de crédito resultante permitiu à CrediFácil categorizar os solicitantes em diferentes níveis de risco. No nosso dataset fake, podemos observar (como esperado, dada a forma como definimos os pontos) que clientes com scores mais altos tendem a ter uma menor proporção de inadimplência.

Essa abordagem permite à CrediFácil tomar decisões mais informadas sobre a concessão de crédito, reduzindo o risco de perdas e oferecendo condições mais adequadas para diferentes perfis de clientes.

**Importante:**

  * **Este é um score de crédito muito simplificado para fins didáticos.** Scores de crédito reais utilizam modelos estatísticos muito mais complexos e um número muito maior de variáveis.
  * **A definição dos pontos e das faixas de risco é crucial e deve ser baseada em análises estatísticas robustas de dados históricos de clientes.**
  * **O monitoramento contínuo do desempenho do score e a sua recalibração são essenciais para garantir a sua eficácia ao longo do tempo.**

Espero que este exemplo prático tenha ajudado a entender melhor a relação entre variáveis estatísticas, o book de variáveis e o score de crédito!

Gostou de desvendar os segredos por trás do score de crédito? Compartilhe este post e deixe sua dúvida ou experiência nos comentários!