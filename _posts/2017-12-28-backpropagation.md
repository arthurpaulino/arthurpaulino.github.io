---
layout: post
title: Backpropagation
tags:
  - machine-learning
  - neural-networks
  - backpropagation
  - python
---

O algoritmo *Backpropagation* pode parecer confuso nas primeiras vezes que o visitamos. Mas neste artigo eu quero cobrir o assunto de forma granulada o suficiente para que sejamos todos capazes de finalmente compreendê-lo.

O objetivo do *Backpropagation* é ajustar os pesos das arestas de uma rede neural para que esta possa responder de forma mais condizente com os dados do conjunto de treinamento.

O ponto chave sobre redes neurais é que elas aprendem com os próprios erros. Nós veremos como isto acontece, mas antes precisamos formalizar uma estrutura de dados para representarmos uma rede neural. Este passo é importante para que possamos acompanhar a lógica do algoritmo **logo após** lidarmos com a matemática necessária.

Se Python lhe é familiar, você se sentirá ainda mais em casa!

# Modelo

O objetivo aqui não é criar o modelo mais eficiente, mas sim o mais didático. Perceba que abstrairemos muitos aspectos de implementação.

## Perceptron

Seja `node` um perceptron.

### Atributos

* `node.bias` é o valor da entrada fixa de `node`

* `node.back_nodes` é a lista de perceptrons que alimentam `node`

* `node.front_nodes` é a lista de perceptrons alimentados por `node`

* `node.output` registra a saída de `node` num contexto em que a rede foi alimentada

## Rede neural

Seja `net` uma rede neural

### Atributos

* `net.output_nodes` é a lista de perceptrons da camada de saída

* `net.all_nodes` é a lista de todos os perceptrons da rede

* `net.w` é o dicionário que contém os pesos das arestas

  `net.w[(node_i, node_j)]` é o peso da aresta que conecta o perceptron `node_i` ao perceptron `node_j`

### Método

* `output_array = net.feed(input_array)` retorna a resposta da rede neural à entrada `input_array`, onde

  * `output_array[i]` é igual a `net.output_nodes[i].output`

# O algoritmo

Assumiremos que todos os perceptrons da rede implementam a sigmóide como função de ativação. Assim, o valor da saída de um perceptron $$j$$ é $$\sigma(s_j) = 1/(1+e^{-s_j})$$, onde $$s_j$$ é a soma das entradas em $$j$$ multiplicadas pelos devidos pesos. Ou seja:

$$s_j = \theta_j + \sum_{b \in B} o_b w_{bj},$$

onde:

* $$\theta_j$$ é o *bias* de $$j$$

* $$B$$ (de $$B$$ack) é o conjunto dos perceptrons que alimentam $$j$$

* $$o_b$$ é a saída do perceptron $$b$$

* $$w_{bj}$$ é o peso da aresta que liga $$b$$ a $$j$$.

Note que $$\frac{d}{ds_j}\sigma(s_j) = \sigma(s_j)[1 - \sigma(s_j)]$$. Este resultado será utilizado mais adiante.

Sejam $$T$$ (de $$T$$arget) a função que desejamos aprender e $$O$$ (de $$O$$utput) a função que a rede computa. Idealmente, gostariamos que $$\forall x, O(x) = T(x)$$. Mas como não conhecemos a lei de formação de $$T$$, precisamos encontrar um caminho para tornarmos $$O$$ o mais semelhante possível a $$T$$.

Definamos então a função $$E = \frac{1}{2}\|O(x) - T(x)\|^2$$ para representar o erro que a rede comete ao tentar simular $$T(x)$$. A estratégia é a seguinte:

1. Utilizar um valor de $$x$$ para o qual conhecemos $$T(x)$$;

    Os valores de $$x$$ que podemos utilizar estão no conjunto de treinamento

2. Encontrar o gradiente de $$E$$ em relação a cada $$w$$ e a cada $$\theta$$ para sabermos exatamente a direção de máximo crescimento do erro para um $$x$$ fixo;

    **Gradiente do erro em relação aos pesos das arestas**

    Para encontrarmos $$\partial E/\partial w_{ij}$$, apliquemos a regra da cadeia:

    $$
      \frac{\partial E}{\partial w_{ij}} =
      \frac{\partial E}{\partial s_j}\frac{\partial s_j}{\partial w_{ij}}
    $$

    Expandindo $$\partial s_j/\partial w_{ij}$$:

    $$
      \frac{\partial s_j}{\partial w_{ij}} = \frac{\partial \bigg(\sum\limits_{b \in B} o_b w_{bj}\bigg)}{\partial w_{ij}} =
    $$

    $$
      = \frac{\partial (o_\xi w_{\xi j} + \dots + o_i w_{ij} + \dots + o_\zeta w_{\zeta j})}{\partial w_{ij}} =
    $$

    $$
      = \stackrel{0}{\frac{\partial (o_\xi w_{\xi j})}{\partial w_{ij}}} + \stackrel{0}{\dots} +
      \frac{\partial (o_i w_{ij})}{\partial w_{ij}} + \stackrel{0}{\dots} +
      \stackrel{0}{\frac{\partial (o_\zeta w_{\zeta j})}{\partial w_{ij}}} =
    $$

    $$
      = \frac{\partial (o_i w_{ij})}{\partial w_{ij}} \stackrel{!!!}{=}
      o_i\frac{\partial w_{ij}}{\partial w_{ij}} = o_i
    $$

    **!!!** Note que $$o_i$$ é constante no contexto em que a entrada da rede está fixa.

    Concluimos então que

    $$\frac{\partial E}{\partial w_{ij}} = \frac{\partial E}{\partial s_j} o_i$$

    Denotaremos $$\partial E/\partial s_j$$ por $$\delta_j$$ para que possamos guardar os valores das componentes do gradiente na matriz $$G$$ fazendo

    $$G_{ij} = \delta_j o_i$$

    **Gradiente do erro em relação aos _biases_**

    Para encontrarmos $$\partial E/\partial \theta_j$$, o processo é semelhante:

    $$
      \frac{\partial E}{\partial \theta_j} =
      \frac{\partial E}{\partial s_j}\frac{\partial s_j}{\partial \theta_j}
    $$

    Já sabemos que $$\partial E/\partial s_j = \delta_j$$. Vamos então expandir $$\partial s_j/\partial \theta_j$$.

    $$
      \frac{\partial s_j}{\partial \theta_j} =
      \frac{\partial\bigg(\theta_j + \sum_\limits{b \in B} o_b w_{bj}\bigg)}{\partial \theta_j} =
      1
    $$

    Portanto,

    $$\frac{\partial E}{\partial \theta_j} = \delta_j$$

3. Ajustar $$w$$ e $$\theta$$ de modo que caminhemos na direção oposta ao gradiente de $$E$$.

    Seja $$\alpha$$ a taxa de aprendizado.

    Uma vez que temos a matriz $$G$$ completa, podemos fazer $$w_{ij} = w_{ij} - \alpha G_{ij}$$.

    Com os valores de $$\delta$$ guardados, podemos fazer $$\theta_j = \theta_j - \alpha\delta_j$$.

## $$\delta$$ para perceptrons da camada de saída

Sejam $$o_i$$ e $$t_i$$ as componentes $$i$$ de $$O(x)$$ e $$T(x)$$, respectivamente, e $$m = dim(O(x)) = dim(T(x))$$. Ao expandirmos a fórmula do erro, obtemos

$$E = \frac{1}{2} \Big\{ \big[ (o_1 - t_1)^2 + \dots + (o_m - t_m)^2 \big]^{\frac{1}{2}} \Big\}^2 =
\frac{1}{2}(o_1 - t_1)^2 + \dots + \frac{1}{2}(o_m - t_m)^2$$

Ao calcularmos $$\delta_j$$, todas as parcelas que não dependem de $$o_j$$ serão anuladas, pois serão tratadas como constantes na derivação parcial de $$E$$ em relação a $$s_j$$. Assim temos

$$\delta_j = \frac{\partial \Big[\frac{1}{2}(o_j - t_j)^2\Big]}{\partial s_j} =
\frac{\partial \Big[\frac{1}{2}(\sigma(s_j) - t_j)^2\Big]}{\partial s_j}$$

Aplicando a regra da cadeia, temos

$$\delta_j = \bigg[\frac{d}{ds_j}\sigma(s_j)\bigg][\sigma(s_j) - t_j]$$

Portanto,

$$\delta_j = \sigma(s_j)[1 - \sigma(s_j)][\sigma(s_j) - t_j] = o_j(1 - o_j)(o_j - t_j)$$

$$G_{ij} = [o_j(1 - o_j)(o_j - t_j)]o_i$$

## Calculando $$\delta$$ indutivamente

Seja $$j$$ um perceptron para o qual queremos encontrar $$\delta_j$$ sendo que sabemos os valores de $$\delta$$ dos perceptrons alimentados por $$j$$.

Imagine que $$j$$ alimenta um perceptron $$f$$ de $$F$$ (de $$F$$ront) por vez. A cada perceptron $$f$$ alimentado, $$j$$ tem uma participação maior na derivada de $$E$$. Então podemos usar a regra da cadeia da seguinte forma:

$$\delta_j = \frac{\partial E}{\partial s_j} =
\sum_{f \in F}\frac{\partial E}{\partial s_f} \frac{\partial s_f}{\partial s_j} =
\sum_{f \in F}\delta_f\frac{\partial s_f}{\partial s_j}$$

Agora precisamos calcular $$\partial s_f/\partial s_j$$

$$\frac{\partial s_f}{\partial s_j} =
\frac{\partial[\sigma(s_\xi) w_{\xi f} + \dots + \sigma(s_j) w_{jf} + \dots + \sigma(s_\zeta) w_{\zeta f}]}{\partial s_j}
\stackrel{!!!}{=} w_{jf}\bigg[\frac{d}{ds_j}\sigma(s_j)\bigg]$$

**!!!** Note que todas as parcelas que não dependem de $$s_j$$ são constantes na derivação. Além disso, $$w_{jf}$$ também é considerado constante. Continuando,

$$\frac{\partial s_f}{\partial s_j} = w_{jf}\bigg[\frac{d}{ds_j}\sigma(s_j)\bigg] =
w_{jf}\sigma(s_j)[1 - \sigma(s_j)] = w_{jf}o_j(1 - o_j)$$

Portanto,

$$\delta_j = \sum_{f \in F}\delta_fw_{jf}o_j(1 - o_j) = o_j(1 - o_j)\sum_{f \in F}\delta_fw_{jf}$$

$$G_{ij} = \Bigg[o_j(1 - o_j)\sum_{f \in F}\delta_fw_{jf}\Bigg]o_i$$

# Implementação do algoritmo

```python
def backpropagation(net, input_array, target_output_array, alpha):

    # capturando a resposta da rede
    output_array = net.feed(input_array)

    # calculando os valores de delta para a camada de saída
    delta = {}
    G = {}
    next_layer = set()
    m = len(net.output_nodes)
    for node, node_order in zip(net.output_nodes, range(m)):

        delta[node] = node.output * (1.0 - node.output) *
            (node.output - target_output_array[node_order])

        # calculando as componentes do gradiente referentes a node
        for back_node in output_node.back_nodes:
            G[(back_node, node)] = delta[node]*back_node.output
            next_layer.add(back_node)

    #calculando os valores de delta indutivamente
    while (len(next_layer) > 0):
        current_layer = next_layer
        next_layer = set()
        while (len(current_layer) > 0):
            node = current_layer.pop()

            if (len(node.back_nodes) == 0):        
                break

            front_sum = 0.0
            for front_node in node.front_nodes:
                front_sum += delta[front_node]*net.w[(node, front_node)]
            delta[node] = node.output*(1 - node.output)*front_sum

            # calculando as componentes do gradiente referentes a node
            for back_node in node.back_nodes:
                G[(back_node, node)] = delta[node]*back_node.output
                next_layer.add(back_node)

    # ajustando os pesos das arestas e os biases
    for edge in net.w:
        net.w[edge] = net.w[edge] - alpha*G[edge]
    for node in net.all_nodes:
        node.bias -= alpha*delta[node]
```

# Bibliografia

ROJAS, Raul. [Neural Networks - A Systematic Introduction](https://page.mi.fu-berlin.de/rojas/neural/). Springer-Verlag, Berlin, New-York, 1996. [p.151-184](https://page.mi.fu-berlin.de/rojas/neural/chapter/K7.pdf).
