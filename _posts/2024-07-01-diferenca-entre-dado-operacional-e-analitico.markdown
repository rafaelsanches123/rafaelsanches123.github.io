---
layout: post
title:  "Diferença entre dado operacional e analítico"
date:   2024-07-01 00:00:00 -0300
categories: data data-analytics
---

![Dados]({{ site.url }}/assets/dados-operacional-x-analitico.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post, vou ensinar para vocês um pouco sobre a diferença entre o que é um dado operacional/transacional e o que um dado analítico. Se você está migrando para área de dados acredito que saber a diferença entre esses 2 tipos de dados pode te ajudar a fazer boas escolhas no futuro sobre qual ferramenta utilizar quando se deparar com algum problema referente a eles no seu dia a dia.

Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

# O que é um dado operacional?

Imagine que você trabalha em uma empresa que vende produtos na internet por meio de um ecommerce. Para manter a sua "Operação" funcionando ou seja você precisa que as informações no seu sistema de informação estejam atualizadas e corretas.

Nesse caso, você teria informações sobre fornecedores, produtos, vendas, clientes entre outras necessárias para que sua operação esteja funcionando.

Essas informações todas precisam estar atualizadas e cada transação realizada nesse sistema precisa garantir que não ocorra falhas e caso isso aconteça a transação deve ser desfeita.

Todo esse cenário apresentado refere se ao dia a dia de uma empresa na qual ela realiza venda de produtos pela internet. Nesse ambiente o seu sistema deve ser capaz de registrar tudo que acontece de forma eficiente e para isso seu banco de dados deve ser bem modelado para garantir otimização e eficiente na hora de armazenar e atualizar as informações dos acontecimentos do dia (operação).

Esses dados no seu banco de dados são dados que registram o que acontece na empresa naquele momento e eles refletem a operação do negócio naquele instante.

De forma resumida dado operacional é aquele que representa o estado atual do negócio naquele momento.

As ferramentas utilizadas para manter esse ambiente funcional se preocupam em conseguir armazenar/atualizar as mudanças dos eventos que ocorrem durante o dia de forma ágil e otimizada. Nesse caso a preocupação é com a escrita, então a sua solução de armazenamento é preparada para realizar essas atividas com o máximo de performance.

# O que é um dado analítico?

Bom, agora que você já sabe o que é um dado operacional, identificar o que é um dado analítico vai ser molezinha.

O dado analítico representa fotos do dado operacional em periodos de tempo distintos no qual você será capaz de analisar esses dados e poder navegar no passado e também tentar prever o futos além de extrair insights valiosos para o seu negócio.

Para tangibilizar o que eu falei anteriormente imagine que todo dia as 24:00 horas os dados do ecommerce mencionados anteriormente são extraídos do sistema operacional/transacional e são movidos para uma outra solucão de armazenamento analítica. Imagina esse processo acontecendo por 1 ano.

Após 1 ano realizando o processo anterior você será capaz de analisar os dados da sua operação num período histórico de 1 ano e vai poder analisar seus dados olhando para dia, mês e ano, sendo assim podendo navegar no passado para entender por exemplo os gostos de clientes que mais compram na sua loja online. Entender suas preferências para oferecer produtos mais assertivos para fechar mais vendas.

Eu poderia ficar mencionando vários e vários outros exemplos, mas acredito que já é suficiente para você entender o que é um dado analítico. Também é importante ressaltar que as tecnologias usadas para trabalhar com os dados analíticos se preocupam mais no aspecto de recuperação e leitura do dado então, a sua performance está mais focada no ambito de ler o dado mais rapido e se preocupa menos na questão da escrita.

Nesse tipo de dado a modelagem também costuma ser diferente pois os dados precisam estar mais próximos pois isso evita ficar cruzando dados armazenados em tabelas diferente o que ajuda na questão da performance de leitura como foi mencionado antes.

# Diferenças

| Dado Operacional                                                                                                  | Dado Analítico                                                                                                                                      |
|-------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Representa o estado atual do negócio (operação) naquele momento                                                                             | Representa fotos do estado do negócio (operação) em diferentes periodos (dia, mês ou ano)                                                                                       |
| Modelagem de Dados otimizada para armazenar o dado de forma eficiente evitando a redundância/duplicação de dados  | Modelagem de Dados otimizada para leitura do dado. Nesse contexto o dado pode ser duplicado pois o foco está na leitura e agregação de informações. |
| Tecnologias: Sistemas de Banco de Dados Transacionais exemplo: SQL Server, Oracle, MySql, Postgress entre outros. | Tecnologias: Sistemas de Data WareHouses e ou Data Lakes.                                                                                           |
