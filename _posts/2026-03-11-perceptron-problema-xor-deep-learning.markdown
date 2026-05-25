--- 
layout: post
title:  "O Perceptron, o Problema do XOR e o Nascimento do Deep Learning"
date:   2026-03-11 09:00:00 -0300
categories: perceptron xor deep-learning redes-neurais
---

![Deep-Learning]({{ site.url }}/assets/deep-learning.png){:style="width: 100%" }

Antes de falarmos sobre Deep Learning, precisamos voltar a 1958.

Foi nesse ano que Frank Rosenblatt apresentou o **Perceptron**, o primeiro modelo de rede neural treinável.

O entusiasmo foi enorme.

Mas alguns anos depois, um problema simples mostrou uma limitação fundamental desse modelo.

Esse problema se chama: **XOR**.

Neste artigo você vai entender:

* O que é o Perceptron
* Como ele funciona matematicamente
* Como implementá-lo em Python
* Por que ele falha no XOR
* Como uma rede com múltiplas camadas resolve o problema

# O que é o Perceptron?

O Perceptron é o modelo mais simples de neurônio artificial.

Ele realiza a seguinte operação:

$y = f(Wx + b)$

Onde:

* $( x ) → $ vetor de entrada
* $( W ) → $ pesos
* $( b ) → $ bias
* $( f ) → $ função degrau (step function)

Ele funciona como um classificador linear.

# O Problema do XOR

A função XOR é definida assim:

| x1 | x2 | Saída |
| -- | -- | ----- |
| 0  | 0  | 0     |
| 0  | 1  | 1     |
| 1  | 0  | 1     |
| 1  | 1  | 0     |

O XOR retorna 1 apenas quando as entradas são diferentes.

Visualmente, os pontos não podem ser separados por uma única reta.

Isso significa:

> O problema XOR **não é linearmente separável**.

E aqui está o ponto crucial:

🚨 O Perceptron só resolve problemas linearmente separáveis.

# Implementando o Perceptron em Python (do zero)

Vamos implementar um Perceptron manualmente usando NumPy.

## Instalação

```bash
pip install numpy
```

## Código

```python
import numpy as np

# Dados do XOR
X = np.array([
    [0, 0],
    [0, 1],
    [1, 0],
    [1, 1]
])

# Respostas referentes ao X
y = np.array([0, 1, 1, 0])

# Inicialização
np.random.seed(42)
weights = np.random.rand(2)
bias = np.random.rand(1)

learning_rate = 0.1
epochs = 20

def step_function(x):
    return 1 if x >= 0 else 0

# Treinamento
for epoch in range(epochs):
    for i in range(len(X)):
        linear_output = np.dot(X[i], weights) + bias
        prediction = step_function(linear_output)
        error = y[i] - prediction
        
        weights += learning_rate * error * X[i]
        bias += learning_rate * error

# Teste
for i in range(len(X)):
    linear_output = np.dot(X[i], weights) + bias
    prediction = step_function(linear_output)
    print(f"Entrada: {X[i]} → Predição: {prediction}")
```

# O Resultado

Você perceberá que:

O modelo **não consegue aprender corretamente o XOR**.

Mesmo após várias épocas, ele não converge para a solução correta.

Isso não é um problema do código.

É um limite matemático do modelo.

# Por que o Perceptron falha?

Porque ele aprende apenas uma fronteira de decisão linear:

$W_1 x_1 + W_2 x_2 + b = 0$

Mas o XOR exige uma separação não linear.

Graficamente, seria necessário algo como duas retas ou uma transformação intermediária.

# A Solução: Múltiplas Camadas

Foi exatamente essa limitação que levou ao desenvolvimento das redes neurais com camadas ocultas.

Com uma camada escondida, conseguimos resolver o XOR:

```python
import torch
import torch.nn as nn
import torch.optim as optim

X = torch.tensor([[0.,0.],[0.,1.],[1.,0.],[1.,1.]])
y = torch.tensor([[0.],[1.],[1.],[0.]])

model = nn.Sequential(
    nn.Linear(2, 4),
    nn.ReLU(),
    nn.Linear(4, 1),
    nn.Sigmoid()
)

criterion = nn.BCELoss()
optimizer = optim.Adam(model.parameters(), lr=0.1)

for epoch in range(2000):
    optimizer.zero_grad()
    output = model(X)
    loss = criterion(output, y)
    loss.backward()
    optimizer.step()

print(model(X))
```

Framework utilizado: PyTorch

Agora o modelo aprende corretamente o XOR.

# Um Marco Histórico

Em 1969, Marvin Minsky e Seymour Papert publicaram o livro
Perceptrons

Nele, demonstraram formalmente a limitação do Perceptron para resolver o XOR.

Isso levou ao chamado “Inverno da IA”.

Décadas depois, com backpropagation e mais poder computacional, as redes neurais profundas ressurgiram — dando origem ao Deep Learning.

# Conclusão

O Perceptron nos ensina algo fundamental:

> Nem todo problema pode ser resolvido com um modelo linear.

O XOR é pequeno.
Mas sua implicação foi gigantesca.

Ele mostrou que precisamos de **profundidade**.