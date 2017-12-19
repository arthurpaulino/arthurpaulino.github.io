---
layout: page
title: Árvores Geradoras Mínimas com Restrição de Grau Mínimo
---

<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

# Descrição do problema

Dados um grafo $$G=(V,E)$$ com pesos atribuídos às arestas, $$C \subset V$$, $$\vert C \vert \geq 1$$, $$T = V \setminus C$$, $$\vert T \vert \geq 2$$ e um número inteiro $$d>0$$, encontrar uma árvore geradora de $$G$$ cuja soma dos pesos de suas arestas seja a menor possível e que atenda às restrições:

* $$\delta(v) \geq d$$, $$\forall v \in C$$;
* $$\delta(v) = 1$$, $$\forall v \in T$$,

onde $$\delta(v)$$ é o grau do vértice $$v$$ na árvore.

# Dificuldade

O problema em estudo é uma generalização do _Caminho Hamiltoniano_. Basta que a entrada possua $$n-2$$ vértices centrais, para os quais o grau mínimo requerido é $$2$$. Portanto, trata-se de um problema _NP-Difícil_.

# A formulação

À cada aresta $$(u,v) \in E$$, associa-se as variáveis $$y*{u,v}$$ se $$u \notin T$$ e $$y*{v,u}$$ se $$v \notin T$$, que podem ser $$0$$ se a aresta não faz parte da solução ou $$1$$ caso contrário.

$$w*{u,v}$$ é o peso da aresta $$(u,v)$$. $$w*{u,v} = w\_{v,u}$$. $$n = \vert V \vert$$.

Por simplicidade de notação, denota-se por $$y_e$$ um variável associada à aresta $$e$$ do problema, analogamente a $$w_e$$.

A ideia é considerar um vértice central $$r$$ como raiz e abstrair um fluxo que parte dele e alcança todos os outros vértices.

A função objetivo é

|\begin{equation}min \sum\_{e \in E} y_e w_e\end{equation}

e as restrições são:

|\begin{equation}\sum*{e \in E} y_e = n-1\end{equation} |||| $$(1)$$
|\begin{equation}\sum*{e \in \delta^+ (\{r\})} y*e \geq d, r \in C\end{equation} |||| $$(2)$$
|\begin{equation}\sum*{e \in \delta^+ (\{v\})} y*e \geq d-1, \forall v \in C\setminus \{r\}\end{equation} |||| $$(3)$$
|\begin{equation}\sum*{e \in (\delta^+ (S) \cap \delta^- (C\setminus S))} y*e \geq 1, \forall S \subset C, r \in S\end{equation} |||| $$(4)$$
|\begin{equation}\sum*{e \in \delta^- (\{t\})} y_e = 1, t \in T\end{equation} |||| $$(5)$$

A restrição $$1$$ exige que haja apenas $$n-1$$ arestas na solução, já que deseja-se uma árvore. $$2$$ e $$3$$ são restrições de fluxo para garantir que o grau mínimo nos vértices centrais seja satisfeito. As restrições $$4$$ garantem a conectividade entre os vértices centrais. $$5$$ são inequações auxiliares para otimizar o trabalho do _solver_.

# Implementação

## Lidando com as restrições $$4$$

Por existirem em quantidade exponencial, é inviável iniciar um modelo prático com todas elas. Portanto adotou-se a estratégia de iniciar o modelo sem elas; verificar se alguma delas foi violada; se sim, inseri-la no modelo e resolvê-lo novamente; se não, o algoritmo acaba.

A separação é feita em tempo polinomial com o algoritmo do corte mínimo, já que $$\sum\_{e \in \delta^+ (S)} y_e$$ é um corte de V. Se o corte mínimo tem valor maior que ou igual a $$1$$, então não há mais restrição $$4$$ violada.

Link para a implementação em C++: [agmrgm](https://github.com/arthurpaulino/agmrgm){:target="\_blank"}.

# Resultados experimentais

Ao relaxar-se a formulação, adimitindo soluções não inteiras, a resolução de inúmeras instâncias foi bastante rápida e, na grande maioria delas, foi atingido o ótimo inteiro. Tal formulação poderá ser utilizada para resolução do problema mais genérico, no qual o conjunto $$C$$ não é derminado na entrada.

# Trabalho futuro

## O grau máximo dos vértices de $$C$$

Em um grafo genérico $$G = (V,E), \vert V \vert = n, \vert E \vert = m$$, tem-se que

|\begin{equation}\sum\_{v \in V} \delta(v) = 2m\end{equation}

Para o problema em estudo, separa-se $$V$$ em $$C$$ e $$T$$. Além disso, $$m = n-1$$:

|\begin{equation}\sum*{v \in C} \delta(v) + \sum*{v \in T} \delta(v) = 2n - 2\end{equation}
|\begin{equation}\delta(u) + \sum*{v \in C\setminus \{u\}} \delta(v) + \vert T \vert = 2n - 2\end{equation}||||$$(5)$$
|\begin{equation}\sum*{v \in C\setminus \{u\}} \delta(v) \geq d(\vert C \vert - 1)\end{equation}
|\begin{equation}\sum\_{v \in C\setminus \{u\}} \delta(v) = d(\vert C \vert - 1) + k, k \geq 0\end{equation}||||$$(6)$$

Substituindo $$6$$ em $$5$$:

|$$\delta(u) + k = 2n - 2 - d(\vert C \vert - 1) - \vert T \vert$$
|$$\delta(u) \leq 2n - 2 - d(\vert C \vert - 1) - \vert T \vert$$
|$$\delta(u) \leq (n - 1) - (d - 1)(\vert C \vert - 1)$$||||$$(7)$$

$$7$$ fornece um limite superior para o grau de todo vértice de $$C$$. Denotaremos tal limitante por $$D$$, que será utilizado na subseção seguinte.

## Comb Inequalities Modificadas (_CIM_'s)

_Comb Inequalities_ são comumente utilizadas para a computação de _ciclos hamiltonianos_. Substituindo-se as inequações $$\delta(v) \leq 2$$ por $$\delta(v) \leq D$$, $$\forall v \in C$$, obtem-se a inequação

|\begin{equation}\sum*{e \in E(H)} y_e + \sum*{i=1}^k \sum*{e \in E(W_i)} \leq \frac{D \vert H \vert - k - 1}{2} + \sum*{i=1}^k (\vert W_i \vert -1)\end{equation} |||| $$(8)$$

Há instâncias cujas relaxações da formulação resultam em soluções não inteiras e que, quando adiciona-se restrições $$8$$ violadas ao modelo, a solução da nova relaxação é inteira.

Diz-se que uma Comb é Simples quando, para todos seus subconjuntos $$W$$, ou $$\vert W \cap H \vert = 1$$, ou $$\vert W \setminus H \vert = 1$$, ou ambas as condições.

Em 2002, Adam N. Letchford and Andrea Lodi propuseram um algoritmo para separação em tempo polinomial de Simple Comb Inequalities. O objetivo, no momento, é analisar e entender tal algoritmo para que ele possa ser adaptado as _CIM_'s violadas.

# Bibliografia

* A. N. Letchford & A. Lodi (2002). _Polynomial-Time Separation of Simple Comb Inequalities_.
* L. A. Wolsey & G. L. Nemhauser (1999). _Integer and Combinatorial Optimization_, Wiley: New York.
