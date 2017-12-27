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

O ponto chave sobre redes neurais é que elas aprendem com os próprios erros. Nós veremos como isto acontece, mas antes precisamos formalizar uma estrutura de dados para representarmos uma rede neural. Este passo é importante para que possamos acompanhar a lógica do algoritmo ao passo que lidamos com a matemática necessária.

Se Python lhe é familiar, você se sentirá ainda mais em casa!

# Modelo

O objetivo aqui não é criar o modelo mais eficiente, mas sim o mais didático. Perceba que abstrairemos muitos aspectos de implementação.

Para simplificarmos ainda mais nossas vidas, assumiremos que todos os perceptrons da rede implementam a função logística $$f(x) = 1/(1+e^{-1})$$ para computarem suas saídas. Note que $$f'(x) = f(x)(1 - f(x))$$, pois este resultado será necessário adiante.

## Perceptron

Seja `node` um perceptron.

### Atributos

* `node.front_nodes` é a lista de perceptrons alimentados por `node`

* `node.back_nodes` é a lista de perceptrons que alimentam `node`

* `node.eval` registra a saída de `node` num contexto em que a rede foi alimentada

## Rede neural

Seja `nn` uma rede neural

### Atributos

* `nn.input_nodes` é a lista de perceptrons da camada de entrada

* `nn.hidden_nodes` é a lista de perceptrons da camada oculta

* `nn.output_nodes` é a lista de perceptrons da camada de saída

* `nn.weight` é a matriz dos pesos das arestas

  Exemplo: `nn.weight[node1][node2]` é o peso da aresta que conecta `node1` a `node2`

### Método

* `output_array = nn.feed(input_array)` retorna a resposta da rede neural à entrada `input_array`, onde

  * `output_array[i]` é igual a `nn.output_nodes[i].eval`

  * `input_array[i]` é a entrada do perceptron `nn.input_nodes[i]`

# O algoritmo

Sejam $$F$$ a função que desejamos aprender e $$N$$ a função que a rede computa. Idealmente, gostariamos que $$\forall x, N(x) = F(x)$$. Mas como não conhecemos a lei de formação de $$F$$, precisamos encontrar outro caminho para tornarmos $$N$$ o mais semelhante a $$F$$ possível.

Definamos então a função $$E(x) = \frac{1}{2}(F(x) - N(x))^2$$ para representar o erro que a rede comete ao tentar simular $$F(x)$$.

Recaptulando, podemos compreender o algoritmo em três etapas:

1. [Alimentar a rede](#alimentando-a-rede) com um elemento do conjunto de treinamento

2. [Calcular o gradiente do erro](#calculando-o-gradiente-do-erro) da rede em relação aos pesos de cada aresta

3. [Atualizar os pesos das arestas](#atualizando-os-pesos-das-arestas) com o intuito de diminuir o erro

## Alimentando a rede

Seja `target_output_array` a resposta ideal para a entrada `input_array`. Nós desejamos que a rede neural `nn` aprenda a dar uma resposta mais próxima de `target_output_array` quando alimentada pela entrada `input_array`.

Primeiramente, nós alimentamos a rede com `input_array` para obtermos `output_array`

```python
output_array = nn.feed(input_array)
```

## Calculando o gradiente do erro

### Perceptrons da camada de saída

### Perceptrons da camada oculta

## Atualizando os pesos das arestas

# Bibliografia

ROJAS, Raul. [Neural Networks - A Systematic Introduction](https://page.mi.fu-berlin.de/rojas/neural/). Springer-Verlag, Berlin, New-York, 1996. [p.151-184](https://page.mi.fu-berlin.de/rojas/neural/chapter/K7.pdf).
