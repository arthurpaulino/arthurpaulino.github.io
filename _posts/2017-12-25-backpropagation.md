---
layout: post
title: Backpropagation descomplicado
tags:
  - machine-learning
  - neural-networks
  - python
---

O algoritmo *Backpropagation* pode parecer confuso nas primeiras vezes que o visitamos. Mas neste artigo eu quero cobrir o assunto de forma granulada o suficiente para que sejamos todos capazes de finalmente compreendê-lo.

O objetivo do *Backpropagation* é ajustar os pesos das arestas de uma rede neural para que esta possa responder de forma mais condizente com os dados do conjunto de treinamento.

O ponto chave sobre redes neurais é que elas aprendem com os próprios erros. Nós veremos como isto acontece, mas antes precisamos formalizar uma estrutura de dados para representarmos uma rede neural. Este passo é importante para que possamos acompanhar a lógica do algoritmo sem que dependamos de uma notação matemática carregada.

Se Python lhe é familiar, você se sentirá ainda mais em casa!

# Modelo

O objetivo aqui não é criar o modelo mais eficiente, mas sim o mais didático. Perceba que abstrairemos muitos aspectos de implementação.

## Rede neural

Seja `nn` uma rede neural

### Atributos

* `nn.input_nodes` é a lista de perceptrons da camada de entrada

* `nn.hidden_nodes` é a lista de perceptrons da camada oculta

* `nn.output_nodes` é a lista de perceptrons da camada de saída

* `nn.weight` é a matriz dos pesos das arestas

  Exemplo: `nn.weight[node1][node2]` é o peso da aresta que conecta `node1` a `node2`

* `nn.eval` é o dicionário que contém as saídas dos perceptrons no contexto em que a rede foi alimentada com uma certa entrada

  Exemplo: `nn.eval[node]` é o valor da saída do perceptron `node`

### Métodos

* `nn.reset()` faz `nn.eval[node] = None` para todos os perceptrons `node` da rede

* `output_array = nn.feed(input_array)` é utilizado para obtermos a resposta da rede neural a uma determinada entrada, onde

  * `output_array[i]` é a saída do perceptron `nn.output_nodes[i]`

  * `input_array[i]` é a entrada do perceptron `nn.input_nodes[i]`

## Perceptron

Seja `node` um perceptron.

### Atributos

* `node.front_nodes` é a lista de perceptrons alimentados por `node`

* `node.back_nodes` é a lista de perceptrons que alimentam `node`

# O algoritmo
