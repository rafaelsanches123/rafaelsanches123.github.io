---
layout: post
title:  "Diferença entre dado operacional e analítico"
date:   2024-07-01 00:00:00 -0300
categories: data data-analytics dado-analítico dado-operacional dado-transacional
---

![Dados]({{ site.url }}/assets/dados-operacional-x-analitico.jpg){:style="width: 100%" }

Fala pessoal blz? Nesse post vou ensinar para vocês a diferença entre dado operacional/transacional e analítico. Se você está migrando para área de dados acredito que conhecer a diferença entre esses dois tipos de dados pode te ajudar a fazer boas escolhas no futuro principalmente sobre qual ferramenta utilizar quando se deparar com algum problema referente a eles no seu dia a dia.

Quer saber mais? Se a respostar for sim, continue comigo nessa leitura!

# O que é um dado operacional?

Imagine que você trabalha em uma empresa que vende produtos na internet por meio de um ecommerce. Para manter a sua __"Operação"__ funcionando, ou seja, você precisa que as informações no seu sistema de informação estejam atualizadas e corretas.

Nesse caso você teria informações sobre fornecedores, produtos, vendas, clientes entre outras necessárias para que sua operação esteja funcionando.

Todas essas informações precisam estar atualizadas e cada transação realizada nesse sistema precisa __garantir__ que não ocorra falhas e caso isso aconteça a transação deve ser desfeita.

Todo esse cenário apresentado refere se ao dia a dia de uma empresa na qual ela realiza venda de produtos pela internet. Nesse ambiente o seu sistema deve ser capaz de registrar tudo que acontece de forma eficiente e para isso seu __banco de dados__ deve ser bem modelado para garantir otimização e eficiência na hora de armazenar e atualizar as informações dos acontecimentos do dia (operação).

Essas informações no seu banco de dados são dados que registram o que acontece na empresa naquele momento/período e eles refletem a operação do negócio naquele instante.

De forma resumida o __dado operacional__ é aquele que representa o __estado atual do negócio naquele momento__.

As ferramentas utilizadas para manter esse ambiente funcional se preocupam em conseguir __armazenar/atualizar__(i.e., registrar) as mudanças dos eventos que ocorrem durante o dia de forma ágil e otimizada no seu banco de dados. Nesse caso a preocupação é com a __escrita__, então a sua solução de armazenamento é preparada para realizar essas atividas com o máximo de performance.

# O que é um dado analítico?

Bom, agora que você já sabe o que é um dado operacional, identificar o que é um dado analítico vai ser molezinha.

O __dado analítico__ representa pedaços do dado operacional em periodos de tempo distintos no qual você será capaz de analisar esses dados e poder voltar no passado e também tentar adivinhar/prever o futuro, além de extrair insights valiosos para o seu negócio e ser capaz de tomar boas decisões baseadas em dados e fatos.

Para tangibilizar o que eu falei anteriormente imagine que todo dia as 24:00 horas os dados do ecommerce mencionados anteriormente são extraídos do sistema operacional/transacional e são movidos para uma outra solucão de armazenamento analítica (e.g., __Data Warehouse/Data Lake__). Imagine esse processo acontecendo por 1 ano.

Após 1 ano realizando o processo anterior você será capaz de analisar os dados da sua operação num período histórico de 12 meses e vai poder analisar seus dados olhando para dia, mês e ano, sendo assim podendo navegar no passado para entender por exemplo os gostos de seus clientes que mais compram na sua loja online. Entender suas preferências para ofertar produtos mais propícios para fechar mais vendas.

Eu poderia ficar aqui mencionando vários, vários e vários outros exemplos, mas acredito que já é suficiente para você entender o que é um dado analítico. Também é importante ressaltar que as tecnologias usadas para trabalhar com os dados analíticos se preocupam mais no aspecto de __recuperação/leitura__ do dado, então a sua performance está mais focada no ambito de ler o dado mais rápido e se preocupa menos na questão da escrita.

Nesse tipo de dado a modelagem também costuma ser diferente pois os dados precisam estar mais próximos pois isso evita ficar cruzando dados (i.e., fazendo JOINs) armazenados em tabelas diferente o que ajuda na questão da performance de leitura como foi mencionado antes.

# Diferenças

| Dado Operacional                                                                                                  | Dado Analítico                                                                                                                                      |
|-------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Representa o estado atual do negócio (operação) naquele momento                                                                             | Representa fotos do estado do negócio (operação) em diferentes periodos (dia, mês ou ano)                                                                                       |
| Modelagem de Dados otimizada para armazenar o dado de forma eficiente evitando a redundância/duplicação de dados  | Modelagem de Dados otimizada para leitura do dado. Nesse contexto o dado pode ser duplicado pois o foco está na leitura e agregação de informações. |
| Tecnologias: Sistemas de Banco de Dados Transacionais exemplo: SQL Server, Oracle, MySql, Postgress entre outros. | Tecnologias: Sistemas de Data WareHouses e ou Data Lakes.                                                                                           |
