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

Para simplificarmos ainda mais nossas vidas, assumiremos que todos os perceptrons da rede implementam a sigmóide $$s(\Sigma) = 1/(1+e^{-\Sigma})$$ para computarem suas saídas, onde $$\Sigma$$ é o resultado da função de agregação do perceptron. Note que $$ds/d\Sigma = s(\Sigma)[1 - s(\Sigma)]$$, pois este resultado será necessário mais adiante.

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

Sejam $$F$$ a função que desejamos aprender e $$N$$ a função que a rede computa. Idealmente, gostariamos que $$\forall x, N(x, w) = F(x)$$, onde $$w$$ é a matriz de pesos das arestas da rede. Mas como não conhecemos a lei de formação de $$F$$, precisamos encontrar um caminho para tornarmos $$N$$ o mais semelhante possível a $$F$$.

Definamos então a função $$E(x, w) = \frac{1}{2}[F(x) - N(x, w)]^2$$ para representar o erro que a rede comete ao tentar simular $$F(x)$$. A estratégia é a seguinte:

1. Utilizar um valor de $$x$$ para o qual conhecemos $$F(x)$$

    Os valores de $$x$$ que podemos utilizar estão no conjunto de treinamento

2. Encontrar o gradiente de $$E(x, w)$$ em relação a cada item $$w_{ij}$$ de $$w$$ para sabermos exatamente a direção de máximo crescimento do erro

    Para encontrarmos $$\partial E/\partial w_{ij}$$, denominemos por $$o_i$$ a saída do perceptron $$i$$ e calculamos a derivada parcial do erro em relação à entrada proveniente de $$i$$:

    $$\frac{\partial E}{\partial(o_i w_{ij})}$$

3. Ajustar $$w$$ de modo que caminhemos na direção oposta ao gradiente de $$E(x, w)$$

Vejamos então como isto é feito na prática.

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
