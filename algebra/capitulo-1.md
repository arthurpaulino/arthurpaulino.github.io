---
layout: page
title: Teoria dos conjuntos e categorias
---

# 1. Teoria ingênua dos conjuntos

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

$$S/\sim$$ é subconjunto de $$\mathscr{P}$$: sejam $$Q$$ um elemento de
$$S/\sim$$ e $$q \in Q$$ tal que $$[q]_\sim = Q$$. Sabemos que existe um único
conjunto $$P \in \mathscr{P}$$ ao qual $$q$$ pertence, pois todos os elementos
de $$S/\sim$$ são formados tão somente por elementos de $$S$$ e $$\mathscr{P}$$
é uma partição de $$S$$. Vamos mostrar que $$Q = P$$ e que, portanto, $$Q \in
\mathscr{P}$$.

* Suponhamos um elemento $$q^* \in Q$$ tal que $$q^* \notin P$$. Como $$q^* \in
Q$$, então $$q^* \sim q$$. Se $$(q^*, q) \in \sim$$ e $$P$$ é o único conjunto
em $$\mathscr{P}$$ ao qual $$q$$ pertence, $$(q^*, q)$$ deve pertencer a $$P
\times P$$ e, portanto, $$q^* \in P$$. Contradição.

* Suponhamos um elemento $$p^* \in P$$ tal que $$p^* \notin Q$$. Como $$p^*$$ e
$$q$$ são elementos de $$P$$, podemos afirmar que $$(p^*, q) \in P \times P$$ e
que, portanto, $$p^* \sim q$$. Já que $$Q = [q]_\sim$$, concluímos que $$p^* \in
Q$$. Contradição.

$$\mathscr{P}$$ é subconjunto de $$S/\sim$$: seja $$P \in \mathscr{P}$$. Vamos
mostrar que existe um conjunto $$Q \in S/\sim$$ com os mesmos elementos de $$P$$
e que, como $$Q = P$$, $$P \in S/\sim$$.

* Seja $$p \in P$$. No produto cartesiano $$P \times P$$ existe um par ordenado
$$(p^*, p)$$ para cada $$p^* \in P$$. Levando esses pares ordenados em
consideração, os quais pertencem a $$\sim$$, construímos $$Q = [p]_\sim$$, que é
formado exatamente pelos elementos ($$p^*$$) de $$P$$. Ora, pela definição de
$$S/\sim$$, $$[p]_\sim$$ deve ser um de seus elementos. Portanto, $$Q \in
S/\sim$$.

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

# 2. Funções entre conjuntos

## Demonstração sugerida pelo autor

> Se a função $$f$$ é injetora e subjetora, então a inversão de $$\Gamma_f$$ é o
grafo de uma função.

Definamos a inversão de $$\Gamma_f$$, $$\Lambda_f$$, como o conjunto:

$$\Lambda_f = \{(b, a) \in B \times A | b = f(a)\}$$

Para mostrarmos que $$\Lambda_f$$ é o grafo de uma função, precisamos provar o
seguinte:

$$\forall b \in B, \exists !a \in A | (b, a) \in \Lambda_f$$

Mas antes de mostrarmos que existe um único $$a$$, mostraremos algo mais fraco:
que existe um $$a$$. Isto é verdade porque $$f$$ é subjetiva, ou seja, deve
existir $$a \in A$$ tal que $$b = f(a)$$ para todo $$b \in B$$.

Agora vamos mostrar que $$a$$ é único para cada $$b \in B$$. Isto é verdade
exatamente porque $$f$$ é injetora, já que elementos diferentes de $$A$$ devem
ser mapeados em elementos diferentes em $$B$$ por $$f$$.

## Proposição 2.1 (1)

> Assume $$A \neq \emptyset$$ and let $$f: A \rightarrow B$$ be a function. Then
f has a left inverse if and only if it is injective.

#### Se $$f$$ tem inversa pela esquerda, então $$f$$ é injetora

Se $$f$$ tem inversa pela esquerda então existe $$g$$ tal que $$g(f(a)) = a$$
para todo $$a \in A$$. Sejam $$a_1$$ e $$a_2$$ elementos de $$A$$ tais que $$a_1
\neq a_2$$. Temos que $$g(f(a_1)) = a_1$$ e $$g(f(a_2)) = a_2$$, ou seja,
$$g(f(a_1)) \neq g(f(a_2))$$.

Se $$f(a_1)$$ fosse igual a $$f(a_2)$$, $$g$$ os enviaria para o mesmo
resultado. Mas o oposto disto deve ocorrer. Então $$f(a_1) \neq f(a_2)$$.

#### Se $$f$$ é injetora, então $$f$$ tem inversa pela esquerda

Construiremos uma função $$g: B \rightarrow A$$ e mostraremos que ela é de fato
uma inversa de $$f$$ pela esquerda. Seja $$s$$ um elemento qualquer de $$A$$
($$A \neq \emptyset$$). Definamos então:

$$g(b) = \begin{cases}a \leftarrow f(a) = b, a \in A\\ s \leftarrow b \notin
\textrm{im}f \end{cases}$$

Primeiramente vejamos por que $$g$$ é de fato uma função. Para qualquer $$b \in
B$$, ou $$b$$ é a imagem de algum $$a \in A$$ segundo $$f$$ ou não é. Em ambos
os casos nós temos um valor para $$g(b)$$ e assim varremos todo o conjunto
$$B$$. Se $$b$$ é tal que se adeque ao segundo caso ($$b \notin \textrm{im}f$$),
o valor de $$g(b)$$ é sempre o mesmo, $$s$$. Caso contrário, pelo fato de $$f$$
ser injetora, não podem existir elementos distintos de $$A$$ que são mapeados
em $$b$$. Logo, $$a$$ é único e portanto $$g$$ é de fato uma função.

Agora vamos verificar se $$g$$ é de fato uma inversa de $$f$$ pela esquerda.
Segundo $$g$$, a imagem de um elemento $$y$$ tal que $$y$$ que é a imagem de um
elemento $$x$$ segundo $$f$$ é o próprio $$x$$. Logo $$g(f(x)) = x$$ e portanto
$$g \circ f$$ é a função identidade.
