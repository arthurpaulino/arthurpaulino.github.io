---
layout: page
title: Preliminares - Teoria dos conjuntos e categorias
---

# Seção 1

## Exercício 1.1

> Locate a discussion of Russell’s paradox, and understand it.

O paradoxo de Russel reside na instanciação de um conjunto, digamos $$R$$,
definido da seguinte forma:

*São elementos de $$R$$ todos os conjuntos que tem eles próprios como elementos,
e nenhum outro.*

Agora, supondo que este conjunto existe, uma das duas afirmações a seguir devem
ser verdadeiras, pois uma é a negação da outra:

1. $$R$$ pertence a si próprio
2. $$R$$ não pertence a si próprio

Acontece que (1) não pode ser verdade, pois, pela própria definição de $$R$$,
este não é composto por conjuntos que pertençam a si próprios.

Então (2) deve ser verdade? Ora, se $$R$$ não pertence a si próprio, então, pela
definição de $$R$$, ele deveria pertencer a si próprio, pois $$R$$ é composto
por **todos** os conjuntos que não têm a si próprios como elementos,
contradição.

Assim, conjunto definido de tal maneira não pode existir.

## Exercício 1.2

> Prove that if $$\sim$$ is an equivalence relation on a set $$S$$, then the
corresponding family $$\mathscr{P}_\sim$$ defined in §1.5 is indeed a partition
of $$S$$: that is, its elements are nonempty, disjoint and their union is $$S$$.

Primeiramente, vamos retomar algumas definições.

A classe de equivalência de um elemento $$a \in S$$, referente à relação de
equivalência $$\sim$$ em $$S$$ e denotada por $$[a]_\sim$$ é o conjunto:

$$[a]_\sim = \{b \in S | b \sim a\}$$

A família $$\mathscr{P}_\sim$$ é o conjunto composto pelas classes de
equivalências formadas com os elementos de $$S$$:

$$\mathscr{P}_\sim = \{[i]_\sim | i \in S\}$$

Queremos provar que $$\mathscr{P}_\sim$$ é uma partição de $$S$$.

1. Os elementos de $$\mathscr{P}_\sim$$ não são vazios:

    $$\sim$$ é reflexiva, então para cada elemento $$i$$ de $$S$$ temos a
    garantia de que a classe de equivalência $$[i]_\sim$$ tem pelo menos o
    elemento $$i$$.

2. Os elementos de $$\mathscr{P}_\sim$$ são disjuntos:

    Suponhamos o contrário, que tais elementos não sejam disjuntos. Então existe
    um elemento $$k$$ pertencente a duas classes de equivalência distintas $$P$$
    e $$Q$$. Se $$P$$ e $$Q$$ são distintas, então sem perda de generalidade
    podemos dizer que existe um elemento $$x \in P$$ que não pertence a $$Q$$.

    Seja $$p \in S$$ o elemento a partir do qual se gerou $$P$$. Portanto $$k
    \sim p$$ e $$x \sim p$$. Como $$\sim$$ é simétrica, então $$p \sim x$$.
    Agora, como $$\sim$$ é transitiva, temos que $$k \sim x$$ e que, por
    simetria, $$x \sim k$$.

    Seja $$q \in S$$ o elemento a partir do qual se gerou $$Q$$. Logo, $$k \sim
    q$$. Ora, se $$x \sim k$$ e $$k \sim q$$, por transitividade temos que $$x
    \sim q$$. Assim, $$x \in Q$$, contradição.

3. A união dos elementos de $$\mathscr{P}_\sim$$, $$U$$, é igual a $$S$$:

    Suponhamos que existe um elemento de $$U$$ que não pertence a $$S$$. Este
    elemento deve pertencer a uma das classes de equivalência de
    $$\mathscr{P}_\sim$$. Segundo a definição de classe de equivalência, todos
    os elementos de $$\mathscr{P}_\sim$$ são conjuntos construídos tão somente
    a partir de elementos de $$S$$. Contradição.

    Agora suponhamos que existe um elemento $$s \in S$$ que não pertence a
    $$U$$. Por reflexividade, temos que $$s \sim s$$. Assim sendo, existe a
    classe de equivalência $$[s]_\sim$$ composta por, pelo menos, o elemento
    $$s$$. Ao realizarmos a operação de união entre todas as classes de
    equivalência de $$S$$ para computarmos $$U$$, o elemento $$s$$ pertencerá a
    $$U$$. Contradição

## Exercício 1.3

> Given a partition $$\mathscr{P}$$ on a set $$S$$, show how to define a
relation $$\sim$$ on $$S$$ such that $$\mathscr{P}$$ is the corresponding
partition.

$$\sim = \bigcup_{P \in \mathscr{P}} P \times P$$

Ou seja, $$\sim$$ é formada pela união dos produtos cartesianos dos elementos de
$$\mathscr{P}$$ por eles mesmos. Agora precisamos mostrar que $$S/\sim =
\mathscr{P}$$.

Sejam $$Q \in S/\sim$$ e $$r \in Q$$. Como $$\mathscr{P}$$ é uma partição de
$$S$$, então existe algum $$P \in \mathscr{P}$$ tal que $$r \in P$$. Se
provarmos que $$Q = P$$, mostramos que todo elemento de $$S$$ pertence aos
mesmos conjuntos tanto em $$S/\sim$$ quanto em $$\mathscr{P}$$. E como cada
elemento destes são formados tão somente por elementos de $$S$$, mostramos que
$$S/\sim$$ e $$\mathscr{P}$$ são formados pelos mesmos elementos, ou seja, são
os mesmos conjuntos.

* $$Q$$ é subconjunto de $$P$$: Suponhamos que existe $$q \in Q$$ tal que $$q
\notin P$$. Como $$q$$ e $$r$$ são elementos de $$Q$$, uma das três opções deve
ser verdadeira: (1) $$r \sim q$$, (2) $$q \sim r$$ ou (3) existe $$q' \in Q$$
tal que $$q \sim q'$$ (3).

    1. $$r \sim q \iff (r, q) \in \sim \iff q \in P$$. Contradição;

    2. $$q \sim r \iff (q, r) \in \sim \iff q \in P$$. Contradição;

    3. $$\exists q' \in Q \vert q \sim q' \implies (q, q') \in \sim \iff q \in
    P$$. Contradição.

    Logo, não pode existir tal $$q$$. Então $$Q \subset P$$.

* $$P$$ é subconjunto de $$Q$$: Suponhamos que existe $$p \in P$$ tal que $$p
\notin Q$$. Como $$p$$ e $$r$$ são elementos de $$P$$, $$(p, r)$$ pertence ao
produto cartesiano $$P \times P$$, logo $$(p, r)$$ pertence à relação $$\sim$$.
Agora, uma das opções a seguir deve ser verdadeira: (1) $$Q$$ é o único elemento
de $$S/\sim$$ ao qual $$r$$ pertence ou (2) existe algum outro conjunto $$Q'
\neq Q$$ pertencente a $$S/\sim$$ ao qual $$r$$ pertence.

    1. 

## Exercício 1.4

> How many different equivalence relations may be defined on the set $$\{1, 2,
3\}$$?

É a mesma quantidade de formas de particionar tal conjunto:

|$$\{\{1, 2, 3\}\}$$
|$$\{\{1\}, \{2, 3\}\}$$
|$$\{\{2\}, \{1, 3\}\}$$
|$$\{\{3\}, \{1, 2\}\}$$
|$$\{\{1\}, \{2\}, \{3\}\}$$
|

Cinco diferentes relações de equivalência podem ser definidas no conjunto $$\{1,
2, 3\}$$. Para um resultado genérico, o número de Bell diz quantas partições
existem em um conjunto com uma quantidade arbitrária de elementos.

## Exercício 1.5

> Give an example of a relation that is reflexive and symmetric, but not
transitive. What happens if you attempt to use this relation to define a
partition on the set?

|$$S = \{1, 2, 3\}$$
|$$\dot\sim = \{(1, 1), (2, 2), (3, 3), (1, 2), (2, 1), (2, 3), (3, 2)\}$$
|$$S/\dot\sim = \{\{1, 2\}, \{1, 2, 3\}, \{2, 3\}\}$$
|

A tentativa de particionar $$S$$ segundo $$\dot\sim$$ não funcionou, pois os
elementos de $$S/\dot\sim$$ não são disjuntos.

## Exercício 1.6

> Define a relation $$\sim$$ on the set $$\mathbb{R}$$ of real numbers, by
setting $$a \sim b \iff b − a \in \mathbb{Z}$$. Prove that this is an
equivalence relation, and find a ‘compelling’ description for
$$\mathbb{R}/\sim$$. Do the same for the relation $$\approx$$ on the plane
$$\mathbb{R} \times \mathbb{R}$$ defined by declaring $$(a_1, a_2) \approx (b_1,
b_2) \iff b_1 − a_1 \in \mathbb{Z}$$ and $$b_2 − a_2 \in \mathbb{Z}$$.

**$$\sim$$ é uma relação de equivalência:**

1. $$\sim$$ é reflexiva: $$\forall x \in \mathbb{R}, x - x = 0 \in \mathbb{Z}
\implies x \sim x$$.

2. $$\sim$$ é simétrica: sejam $$x_1$$ e $$x_2$$ números reais tais que $$x_1
\sim x_2$$. Logo, $$x_2 - x_1 = z \in \mathbb{Z}$$. Ora, $$-z$$ também é um
número inteiro pois é o produto de dois números inteiros, então $$x_1 - x_2 \in
\mathbb{Z}$$ e portanto $$x_2 \sim x_1$$.

3. $$\sim$$ é transitiva: sejam $$x_1$$, $$x_2$$ e $$x_3$$ números reais tais
que $$x_1 \sim x_2$$ e $$x_2 \sim x_3$$. Sejam também $$z_1 = x_2 - x_1$$ e
$$z_2 = x_3 - x_2$$ números inteiros (devido à definição de $$\sim$$). Acontece
que $$z_3 = z_2 + z_1$$ é a soma de dois inteiros e portanto também é um
inteiro. Desenvolvendo: $$z_3 = x_3 - x_2 + x_2 - x_1 = x_3 - x_1 \in
\mathbb{Z}$$. Portanto, $$x_1 \sim x_3$$.

Uma possível descrição de $$\mathbb{R}/\sim$$ é um conjunto cujos elementos são
as classes de equivalência de cada $$\epsilon$$ real pertencente ao intervalo
$$[0, 1)$$. Cada uma dessas classes é formada por todos os números reais cujas
distâncias até o $$\epsilon$$ referente são inteiras:

$$\mathbb{R}/\sim = \{[\epsilon]_\sim | 0 \leq \epsilon < 1\}$$

**$$\approx$$ é uma relação de equivalência:**

1. $$\approx$$ é reflexiva: $$\forall x, y \in \mathbb{R}, x - x = y - y = 0
\in \mathbb{Z} \implies (x, y) \approx (x, y)$$.

2. $$\approx$$ é simétrica: sejam $$x_1$$, $$x_2$$, $$y_1$$ e $$y_2$$ números
reais tais que $$(x_1, y_1) \approx (x_2, y_2)$$. Logo, $$x_2 - x_1 = z_x \in
\mathbb{Z}$$ e $$y_2 - y_1 = z_y \in \mathbb{Z}$$. Ora, tanto $$-z_x$$ quanto
$$-z_y$$ também são inteiros pois são produtos de dois números inteiros. Então
$$x_1 - x_2 \in \mathbb{Z}$$ e $$y_1 - y_2 \in \mathbb{Z}$$, logo $$(x_2, y_2)
\approx (x_1, y_1)$$.

3. $$\approx$$ é transitiva: sejam $$x_1$$, $$x_2$$, $$x_3$$, $$y_1$$, $$y_2$$ e
$$y_3$$ números reais tais que $$(x_1, x_2) \approx (x_2, y_2)$$ e $$(x_2, y_2)
\approx (x_3, y_3)$$. Sejam também $$z_{x_1} = x_2 - x_1$$, $$z_{x_2} = x_3 -
x_2$$ e $$z_{y_1} = y_2 - y_1$$, $$z_{y_2} = y_3 - y_2$$ números inteiros
(devido à definição de $$\approx$$). Acontece que tanto $$z_{x_3} = z_{x_2} +
z_{x_1}$$ quanto $$z_{y_3} = z_{y_2} + z_{y_1}$$ são somas de dois inteiros,
cada um, e portanto também são inteiros. Desenvolvendo:

|$$z_{x_3} = x_3 - x_2 + x_2 - x_1 = x_3 - x_1 \in \mathbb{Z}$$
|$$z_{y_3} = y_3 - y_2 + y_2 - y_1 = y_3 - y_1 \in \mathbb{Z}$$
|

Então $$(x_1, y_1) \approx (x_3, y_3)$$.

Uma descrição para $$\mathbb{R^2}/\approx$$ é o conjunto formado pelas classes
de equivalência geradas a partir de pares $$(\epsilon_x, \epsilon_y)$$, de modo
que tanto $$\epsilon_x$$ quanto $$\epsilon_y$$ pertencentem ao intervalo $$[0,
1)$$. Cada par $$(\epsilon_x, \epsilon_y)$$ gera uma classe de equivalência que
contém os pontos pertencentes aos cruzamentos de um *grid* em $$\mathbb{R^2}$$
centralizado em $$(\epsilon_x, \epsilon_y)$$:

$$\mathbb{R}/\approx = \{[(\epsilon_x, \epsilon_y)]_\approx | 0 \leq \epsilon_x
< 1 \wedge 0 \leq \epsilon_y < 1\}$$

---
