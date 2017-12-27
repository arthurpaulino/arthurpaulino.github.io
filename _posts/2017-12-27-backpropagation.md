---
layout: post
title: Backpropagation
tags:
  - machine-learning
  - neural-networks
  - python
---

O algoritmo *Backpropagation* pode parecer confuso nas primeiras vezes que o visitamos. Mas neste artigo eu quero cobrir o assunto de forma granulada o suficiente para que sejamos todos capazes de finalmente compreendê-lo.

O objetivo do *Backpropagation* é ajustar os pesos das arestas de uma rede neural para que esta possa responder de forma mais condizente com os dados do conjunto de treinamento.

O ponto chave sobre redes neurais é que elas aprendem com os próprios erros. Nós veremos como isto acontece, mas antes precisamos formalizar uma estrutura de dados para representarmos uma rede neural. Este passo é importante para que possamos acompanhar a lógica do algoritmo logo após lidarmos com a matemática necessária.

Se Python lhe é familiar, você se sentirá ainda mais em casa!

# Modelo

O objetivo aqui não é criar o modelo mais eficiente, mas sim o mais didático. Perceba que abstrairemos muitos aspectos de implementação.

## Perceptron

Seja `node` um perceptron.

### Atributos

* `node.back_nodes` é a lista de perceptrons que alimentam `node`

* `node.front_nodes` é a lista de perceptrons alimentados por `node`

* `node.eval` registra a saída de `node` num contexto em que a rede foi alimentada

## Rede neural

Seja `net` uma rede neural

### Atributos

* `net.output_nodes` é a lista de perceptrons da camada de saída

* `net.w` é o dicionário que contém os pesos das arestas

  `net.w[(node_i, node_j)]` é o peso da aresta que conecta o perceptron `node_i` ao perceptron `node_j`

### Método

* `output_array = net.feed(input_array)` retorna a resposta da rede neural à entrada `input_array`, onde

  * `output_array[i]` é igual a `net.output_nodes[i].eval`

# O algoritmo

Assumiremos que todos os perceptrons da rede implementam a sigmóide como função de ativação. Assim, o valor da saída de um perceptron $$j$$ é $$s(a_j) = 1/(1+e^{-a_j})$$, onde $$a_j$$ é o resultado das entradas em $$j$$ multiplicadas pelos devidos pesos. Ou seja:

$$a_j = \sum\limits_{k \in B} o_k w_{kj},$$

onde:
* $$B$$ é o conjunto dos perceptrons que alimentam $$j$$

* $$o_k$$ é a saída do perceptron $$k$$

* $$w_{kj}$$ é o peso da aresta que liga $$k$$ a $$j$$.

Note que $$\frac{d}{da_j}s(a_j) = s(a_j)[1 - s(a_j)]$$. Este resultado será utilizado mais adiante.

Sejam $$F$$ a função que desejamos aprender e $$N$$ a função que a rede computa. Idealmente, gostariamos que $$\forall x, N(x, w) = F(x)$$, onde $$w$$ é a matriz de pesos das arestas da rede. Mas como não conhecemos a lei de formação de $$F$$, precisamos encontrar um caminho para tornarmos $$N$$ o mais semelhante possível a $$F$$.

Definamos então a função $$E = \frac{1}{2}\|N(x) - F(x)\|^2$$ para representar o erro que a rede comete ao tentar simular $$F(x)$$. A estratégia é a seguinte:

1. Utilizar um valor de $$x$$ para o qual conhecemos $$F(x)$$

    Os valores de $$x$$ que podemos utilizar estão no conjunto de treinamento

2. Encontrar o gradiente de $$E$$ em relação a cada item $$w_{ij}$$ de $$w$$ para sabermos exatamente a direção de máximo crescimento do erro para um $$x$$ fixo

    Para encontrarmos $$\partial E/\partial w_{ij}$$, apliquemos a regra da cadeia:

    $$
      \frac{\partial E}{\partial w_{ij}} =
      \frac{\partial E}{\partial a_j}\frac{\partial a_j}{\partial w_{ij}}
    $$

    Expandindo $$\partial a_j/\partial w_{ij}$$:

    $$
      \frac{\partial a_j}{\partial w_{ij}} =
      \frac{\partial \bigg(\sum\limits_{k \in B} o_k w_{kj}\bigg)}{\partial w_{ij}} =
    $$

    $$
      = \frac{\partial (o_\lambda w_{\lambda j} + \dots + o_i w_{ij} + \dots + o_\eta w_{\eta j})}{\partial w_{ij}} =
    $$

    $$
      = \stackrel{0}{\frac{\partial (o_\lambda w_{\lambda j})}{\partial w_{ij}}} + \stackrel{0}{\dots} +
      \frac{\partial (o_i w_{ij})}{\partial w_{ij}} + \stackrel{0}{\dots} +
      \stackrel{0}{\frac{\partial (o_\eta w_{\eta j})}{\partial w_{ij}}} =
    $$

    $$
      = \frac{\partial (o_i w_{ij})}{\partial w_{ij}} \stackrel{!!!}{=}
      o_i\frac{\partial w_{ij}}{\partial w_{ij}} = o_i
    $$

    **!!!** Note que $$o_i$$ é constante no contexto em que a entrada da rede está fixa.

    Concluimos então que

    $$\frac{\partial E}{\partial w_{ij}} = \frac{\partial E}{\partial a_j} o_i$$

    Denotaremos $$\partial E/\partial a_j$$ por $$\delta_j$$ para que possamos guardar os valores das componentes do gradiente na matriz $$G$$ fazendo

    $$G_{ij} = \delta_j o_i$$

3. Ajustar $$w$$ de modo que caminhemos na direção oposta ao gradiente de $$E$$

    Uma vez que temos a matriz $$G$$ completa, podemos fazer $$w_{ij} = w_{ij} - \alpha G_{ij}$$, onde $$\alpha$$ é a taxa de aprendizado.

## $$\delta$$ para perceptrons da camada de saída

Sejam $$o_i$$ e $$t_i$$ as componentes $$i$$ de $$N(x)$$ e $$F(x)$$ respectivamente, e $$m$$ a dimensão de $$N(x)$$ e de $$F(x)$$. Ao expandirmos a fórmula do erro, obtemos

$$E = \frac{1}{2} \Big\{ \big[ (o_1 - t_1)^2 + \dots + (o_m - t_m)^2 \big]^{\frac{1}{2}} \Big\}^2 =
\frac{1}{2}(o_1 - t_1)^2 + \dots + \frac{1}{2}(o_m - t_m)^2$$

Ao calcularmos $$\delta_j$$, todas as parcelas que não dependem de $$o_j$$ serão anuladas, pois serão tratadas como constantes na derivação parcial de $$E$$ em relação a $$a_j$$. Assim temos

$$\delta_j = \frac{\partial \Big[\frac{1}{2}(o_j - t_j)^2\Big]}{\partial a_j} =
\frac{\partial \Big[\frac{1}{2}(s(a_j) - t_j)^2\Big]}{\partial a_j}$$

Aplicando a regra da cadeia, temos

$$\delta_j = \bigg[\frac{d}{da_j}s(a_j)\bigg][s(a_j) - t_j]$$

Portanto

$$\delta_j = s(a_j)[1 - s(a_j)][s(a_j) - t_j] = o_j(1 - o_j)(o_j - t_j)$$

$$G_{ij} = o_j(1 - o_j)(o_j - t_j)o_i$$

## $$\delta$$ para perceptrons da camada oculta

# Implementação do algoritmo

## Alimentando a rede

Seja `target_output_array` a resposta ideal para a entrada `input_array`. Nós desejamos que a rede neural `net` aprenda a dar uma resposta mais próxima de `target_output_array` quando alimentada pela entrada `input_array`.

Primeiramente, nós alimentamos a rede com `input_array` para obtermos `output_array`

```python
output_array = net.feed(input_array)
```

## Calculando o gradiente do erro

Aqui nós utilizaremos um dicionário `d` para guardar os valores $$\delta$$ de cada perceptron.

Utilizaremos também `G`, um dicionário semelhante à estrutura que guarda os pesos das arestas de `net`.

```python
output_array = net.feed(input_array)

d = {}
for node in net.hidden_nodes + net.output_nodes:
    d[node] = 0.0

G = {}
for edge in net.w:
    G[edge] = 0.0
```

### Perceptrons da camada de saída

```python
output_array = net.feed(input_array)

d = {}
for node in net.hidden_nodes + net.output_nodes:
    d[node] = 0.0

G = {}
for edge in net.w:
    G[edge] = 0.0

m = len(net.output_nodes)
for output_node, node_order in zip(net.output_nodes, range(m)):

    d[output_node] = output_node.eval *
        (1.0 - output_node.eval) *
        (output_node.eval - target_output_array[node_order])

    for back_node in output_node.back_nodes:
        G[(back_node, output_node)] = d[output_node]*back_node
```

### Perceptrons da camada oculta

```python
output_array = net.feed(input_array)

d = {}
for node in net.hidden_nodes + net.output_nodes:
    d[node] = 0.0

G = {}
for edge in net.w:
    G[edge] = 0.0

m = len(net.output_nodes)
for output_node, node_order in zip(net.output_nodes, range(m)):

    d[output_node] = output_node.eval *
        (1.0 - output_node.eval) *
        (output_node.eval - target_output_array[node_order])

    for back_node in output_node.back_nodes:
        G[(back_node, output_node)] = d[output_node]*back_node

#####
...
#####
```

## Atualizando os pesos das arestas

```python
output_array = net.feed(input_array)

d = {}
for node in net.hidden_nodes + net.output_nodes:
    d[node] = 0.0

G = {}
for edge in net.w:
    G[edge] = 0.0

m = len(net.output_nodes)
for output_node, node_order in zip(net.output_nodes, range(m)):

    d[output_node] = output_node.eval *
        (1.0 - output_node.eval) *
        (output_node.eval - target_output_array[node_order])

    for back_node in output_node.back_nodes:
        G[(back_node, output_node)] = d[output_node]*back_node

#####
...
#####

alpha = 0.1
for edge in net.w:
    net.w[edge] = net.w[edge] - alpha*G[edge]
```

# Bibliografia

ROJAS, Raul. [Neural Networks - A Systematic Introduction](https://page.mi.fu-berlin.de/rojas/neural/). Springer-Verlag, Berlin, New-York, 1996. [p.151-184](https://page.mi.fu-berlin.de/rojas/neural/chapter/K7.pdf).
