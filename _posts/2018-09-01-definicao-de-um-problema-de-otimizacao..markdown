---
layout: post
title:  "O que é um problema de otimização?"
date:   2018-09-01 17:33:03 -0300
categories: otimização
---

![otimização]({{ site.url }}/assets/otimizacao.jpg)

Um problema de ótimização pode ser tanto de minimização (i.e., tentar reduzir algo) ou de máximização (i.e., tentar aumentar algo). Além disso, um problema de otimização pode ter dados discretos ou contínuos.

Problemas de ótimização também podem ser mono-objetivo (i.e., possui apenas uma função objetivo) ou multi-objetivos (possui mais de uma função objetivo).

Segundo Deb (2001), Ringuest (2012), Collette e Siarry (2013), um problema de otimização multi-objetivo pode ser formulado da seguinte forma:

* Tem-se $ f_{i}(X) $ onde, $ (i=1, 2, 3, ..., q) $ e $f$ representa um conjunto de __funções objetivo__ a serem otimizadas e $ X $ representa os parâmetros a serem otimizados dessa função (i.e., variaveis de decisão do problema a ser otimizado). Além disso, $ q $ representa a __quantidade de funções objetivo__ a serem otimizadas;

* Para um problema __mono-objetivo__ apenas seria fixado que o mesmo trabalha apenas com uma função objetivo e expressão seria desse modo $ f_{1}(X) $ diferente da apresentada no item acima;

* Sabe-se que $X$ é formado por $(x1, x2, x3, ..., xD)$ __variáveis de decisão__ onde, $ D $ representa a quantidade de variáveis a serem otimizadas;

* Sabe-se que para cada função $ f_{i}(X) $ __pode haver várias restrições__ $ g(X) $ impostas para elas delimitando as soluções consideradas factíveis (i.e., soluções corretas que estejam dentro das reestrições estabelecidas para o problema a ser solunionado) ao problema multi-objetivo;

* $X ∈ Ω$ onde, $Ω$ representa o __espaço de busca do problema__ de otimização.

Com base nos trabalhos de Deb (2001), Ringuest (2012), Collette e Siarry (2013), os conceitos mais comuns a qualquer metodologia de otimização serão apresentados a seguir:

__Função Objetivo__: equação matemática que representa o que se deseja melhorar (minimizar ou maximizar). Tem como sinônimos: critério de otimização, função de custo ou ainda função de mérito (fitness function);

__Parâmetros__: correspondem às variáveis da função objetivo. São ajustados durante o processo de otimização visando obter a(s) solução(ões) ótima(s). Além disso, podem ser chamados de variáveis de otimização;

__Espaço de busca__: domínio (delimitado ou não) que contém os valores dos parâmetros. Corresponde ao espaço de soluções. A dimensão do espaço de busca é definida pelo número de parâmetros envolvidos nas soluções (por exemplo, se cada solução é formada por três parâmetros, o espaço de busca é tridimensional);

__Espaço de objetivos__: conjunto imagem do espaço de busca determinado por todos os valores possíveis das funções objetivo;

__Restrições__: especificações do problema que delimitam os espaços de parâmetros e que não permitem determinada faixa de valores nos objetivos e.g., para determinado problema, pode-se impor que abaixo de certo valor a solução não seja considerada válida;

__Solução ótima local__: solução encontrada no espaço de busca em uma determinada região na qual, esta é considera a melhor de todas as soluções descobertas naquela região;

__Solução ótima global__: diferente da solução ótima local, a solução ótima global é aquela na qual nenhuma outra solução consegue ser melhor que ela, ou seja, em todas as regiões do espaço de busca, essa solução é, melhor que qualquer outra independente de onde essa solução esteja no espaço de busca.

## Exemplo de um problema de otimização que utiliza variáveis discretas:

O Caixeiro Viajante (CV) é um problema de otimização combinatória (i.e., utiliza variáveis discretas) bastante conhecido na área da ciência da computação. Esse problema é considerado simples de ser explanado mas, muito difícil de ser resolvido em tempo polinomial dependendo da quantidade de cidades utilizadas no problema e uma vez que o número de cidades aumenta, a complexidade do problema aumenta também. Ele é um problema que cresce expônenciamente a medida que mais cidades vão sendo adicionadas ao problema.

__Problema do CV__: um vendedor ambulante defini uma cidade para começar a vender seus produtos e ele deseja visitar outras cidades passando por uma a uma sem repetir nenhuma delas sendo que ao visitar todas as cidades da região que ele se encontra ele deve retornar para cidade inicial na qual ele começou seu trajeto de vendas.

__Objetivo do problema__: minimizar o custo da distância gasta para visitar todas as cidades e retornar para a cidade inicial. Nesse caso, o objeto então é encontrar a melhor sequência para se visitar as cidades e que gaste a menor distância possível. 

__Formulação do problema__:

* Variáveis de Decisão: $C_{i}$ tal que, $ (i = 1,...,D) $ onde, $D$ representa o número de cidades do problema do CV;

* Uma vez que você tenha as coordenadas das cidades, você precisa aplicar algum método para calcular as distâncias entre elas e um dos métodos mais conhecido na literatura é a __distância euclidiana__;

* 

### Referências

DEB, K. Multi-objective optimization using evolutionary algorithms. John Wiley & Sons,2001.

RINGUEST, J. L. Multiobjective optimization: behavioral and computational considerations. Springer Science & Business Media, 2012.

COLLETTE, Y.; SIARRY, P. Multiobjective optimization: principles and case studies. Springer Science & Business Media, 2013.