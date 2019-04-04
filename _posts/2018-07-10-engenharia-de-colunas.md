---
layout: post
title: Engenharia de Colunas
subtitle: Uma Arte na Ciência de Dados
tags:
  - data-science
  - feature-engineering
---

Vamos estudar um pouco sobre esse assunto tão raramente falado em cursos, tutoriais,
livros etc. O desafio de se falar de engenharia de colunas é que cada base de dados
é um mundo cheio de particularidades e portanto merece seus próprios *insights*. Mas
é por isso que eu digo que a engenharia de colunas é uma Arte na Ciência de Dados:
porque é nessa fase que a nossa expressividade matemática ganha asas.

Para notarmos a importância deste processo, basta observarmos o andamento de algumas
[competições no Kaggle](https://www.kaggle.com/competitions){:target="\_blank"} ou de qualquer projeto
de médio porte (ou maior) de Ciência de Dados. Salta aos olhos o quão pouco dos
esforços é direcionado à modelagem se compararmos com o zelo empreendido na fase
de tratamento dos dados. Pode parecer estranho para alguns, mas minha maior
recomendação prática para se iniciar na área é conquistar um bom domínio da biblioteca
de gerenciamento de dados de sua escolha.

Outra grande lição que aprendi foi a seguinte: **não ter uma perspectiva fria a
respeito dos dados**. Quando vamos encarar um problema que queremos resolver com
Aprendizagem de Máquina, precisamos aprender as especificidades da área para que
possamos fornecer informações ricas o suficiente para os nossos modelos, pois um
modelo só será tão bom quanto a qualidade dos dados que ele processa.

Portanto, o motivo pelo qual eu decidi escrever este post foi elencar algumas
possibilidades de engenharia de colunas. Novamente ressalto que cada base de dados
é única, mas vejamos se podemos traçar algumas estratégias em linhas gerais.

# Coordenadas geográficas

Até onde minha experiência vai, percebo que coordenadas são armazenadas com duas
finalidades principais:

- Registrar pontos de partida e de chegada
- Registrar locais de ocorrência

## Pontos de partida e de chegada

Para problemas em áreas pequenas (ex.: dentro de uma cidade), podemos criar uma
coluna nova com a [distância Manhattan](https://en.wikipedia.org/wiki/Taxicab_geometry){:target="\_blank"},
excelente para explicitar aproximações de distâncias em áreas urbanas.

![](https://upload.wikimedia.org/wikipedia/commons/0/08/Manhattan_distance.svg){:class="img-responsive"}
*Fonte: [Wikipedia](https://en.wikipedia.org/wiki/Taxicab_geometry){:target="\_blank"}*

Quando o problema envolve áreas maiores, como estados ou países, já precisamos nos
preocupar com as distorções causadas pela superfície esférica do planeta. Portanto
podemos utilizar a [fórmula Haversine](https://en.wikipedia.org/wiki/Haversine_formula){:target="\_blank"}
(em Python [aqui](https://rosettacode.org/wiki/Haversine_formula#Python){:target="\_blank"})

![](https://upload.wikimedia.org/wikipedia/commons/3/38/Law-of-haversines.svg){:class="img-responsive"}
*Fonte: [Wikipedia](https://en.wikipedia.org/wiki/Haversine_formula){:target="\_blank"}*

## Locais de ocorrência

Nesse caso, podemos verificar se é possível observar padrões na manifestação do
fenômeno estudado ao longo da superfície. Algo que gosto de fazer é utilizar
[clusterização](https://en.wikipedia.org/wiki/Cluster_analysis){:target="\_blank"}
e métodos de visualização para validar esta hipótese. Desta forma, podemos criar
etiquetas para cada cluster e as utilizarmos em uma coluna categórica.

Seguem alguns links para kernels que eu escrevi e que envolvem clusterização e
visualizações.

- [Data Science with Compassion](https://www.kaggle.com/arthurpaulino/data-science-with-compassion){:target="\_blank"}
- [Spatial analysis tutorial](https://www.kaggle.com/arthurpaulino/spatial-analysis-tutorial){:target="\_blank"}

# Timestamps

Marcações temporais são bastante versáteis. A depender do tipo de problema, podemos
usar o conjunto de treinamento para respondermos algumas perguntas:

- O fenômeno estudado apresenta alguma periodicidade?
- O fenômeno estudado se comporta de forma muito diferente nos feriados?
- Eventos mais recentes têm maior peso que os mais antigos?

A ideia é transformar estas perguntas em colunas que as respondam para então fazer
validações visuais ou estatísticas.

# Bases de dados auxiliares

Quando começamos a estudar Data Science, normalmente nos deparamos com bases de
dados já mastigadas, resumidas em uma única tabela (ou no máximo duas, treino e
teste, com praticamente as mesmas colunas). Mas sejamos realistas: **nos desafios
cotidianos de um cientista de dados raramente encontramos esta facilidade**. Cabe
a nós entender os relacionamentos entre as diferentes tabelas e extrairmos os dados
necessários para gerarmos a tabela compilada que planejarmos.

## Exemplo: risco de crédito

Temos uma tabela de empréstimos ativos (uma linha por empréstimo) e outra tabela
contendo todos os empréstimos anteriores de todos os clientes. Queremos saber se
os cliente pagarão os empréstimos ativos devidamente. Nesse caso nós podemos
enriquecer os dados da tabela principal com dados da tabela auxiliar. Mas como,
exatamente? Funções de agregação!

Agrupamos os dados da tabela auxiliar por cliente e aplicamos funções de agregação
nas outras colunas: somas, médias, contagens, desvios padrões, máximos, mínimos
etc. Claro que não usamos todas as funções de agregação em todas as colunas… deveremos
fazer a escolha baseada em conhecimentos específicos da área do problema. Quantos
empréstimos o cliente já fez? Qual o seu índice de inadimplência? Este índice vem
aumentando ou diminuindo com o tempo? A quantia envolvida no empréstimo atual difere
muito da quantia usual dos empréstimos anteriores? E assim por diante…

# Conclusão

Como podemos ver, engenharia de colunas é uma área vasta e cheia de possibilidades.
Mas não posso deixar de dizer que cada coluna criada deve passar por um rigoroso
processo de validação para sabermos se estamos criando redundância ou capturando
informação de fato. E em última análise, a nova coluna realmente capacita o modelo
escolhido a alcançar uma maior acurácia?

Vale ressaltar que engenharia de colunas depende bastante da experiência do cientista
de dados. A prática é fundamental. Uma leitura como essa pode ser esclarecedora,
mas nada substitui aquelas horas quebrando cabeça para melhorar a acurácia dos seus
modelos.
