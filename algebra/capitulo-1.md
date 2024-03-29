---
layout: page
title: Teoria dos conjuntos e categorias
---

# 1. Teoria ingênua dos conjuntos

## Exercício 1.1

> Encontre uma discussão acerca do paradoxo de Russel e o entenda.

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
> Prove que se $$\sim$$ é uma relação de equivalência no conjunto $$S$$, então
a família correspondente $$\mathscr{P}_\sim$$ definida em §1.5 é de fato uma
partição de $$S$$: ou seja, seus elementos são não-vazios, disjuntos e suas
uniões resulta no próprio $$S$$.

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

> Dada uma partição $$\mathscr{P}$$ no conjunto $$S$$, mostre como definir uma
relação $$\sim$$ em $$S$$ tal que $$\mathscr{P}$$ é sua partição correspondente.

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

> Quantas diferentes relações de equivalência podem ser definidas no conjunto
$$\{1, 2, 3\}$$?

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

> Dê um exemplo de uma relação que é reflexiva, simétrica, mas não transitiva.
O que acontece se você tentar usar esta relação para definir uma partição no
conjunto?

|$$S = \{1, 2, 3\}$$
|$$\dot\sim = \{(1, 1), (2, 2), (3, 3), (1, 2), (2, 1), (2, 3), (3, 2)\}$$
|$$S/\dot\sim = \{\{1, 2\}, \{1, 2, 3\}, \{2, 3\}\}$$
|

A tentativa de particionar $$S$$ segundo $$\dot\sim$$ não funcionou, pois os
elementos de $$S/\dot\sim$$ não são disjuntos.

## Exercício 1.6

> Defina uma relação $$\sim$$ no conjunto $$\mathbb{R}$$ dos números reais tal
que $$a \sim b \iff b − a \in \mathbb{Z}$$. Prove que se trata de uma relação
de equivalência e encontre uma descrição convincente para $$\mathbb{R}/\sim$$.
Faça o mesmo para a relação $$\approx$$ no plano $$\mathbb{R} \times
\mathbb{R}$$ definida por $$(a_1, a_2) \approx (b_1, b_2) \iff b_1 − a_1 \in
\mathbb{Z}$$ e $$b_2 − a_2 \in \mathbb{Z}$$.

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

> Se a função $$f$$ é injetora e sobrejetora, então a inversão de $$\Gamma_f$$ é
o grafo de uma função.

Definamos a inversão de $$\Gamma_f$$, $$\Lambda_f$$, como o conjunto:

$$\Lambda_f = \{(b, a) \in B \times A | b = f(a)\}$$

Para mostrarmos que $$\Lambda_f$$ é o grafo de uma função, precisamos provar o
seguinte:

$$\forall b \in B, \exists !a \in A | (b, a) \in \Lambda_f$$

Mas antes de mostrarmos que existe um único $$a$$, mostraremos algo mais fraco:
que existe um $$a$$. Isto é verdade porque $$f$$ é sobrejetora, ou seja, deve
existir $$a \in A$$ tal que $$b = f(a)$$ para todo $$b \in B$$.

Agora vamos mostrar que $$a$$ é único para cada $$b \in B$$. Isto é verdade
exatamente porque $$f$$ é injetora, já que elementos diferentes de $$A$$ devem
ser mapeados em elementos diferentes em $$B$$ por $$f$$.

## Proposição 2.1 (1)

> Assuma $$A \neq \emptyset$$ e seja $$f: A \rightarrow B$$ uma função. Então
$$f$$ tem uma inversa pela esquerda se, e somente se, ela é injetora.

### Se $$f$$ tem inversa pela esquerda, então $$f$$ é injetora

Se $$f$$ tem inversa pela esquerda então existe $$g$$ tal que $$g(f(a)) = a$$
para todo $$a \in A$$. Sejam $$a_1$$ e $$a_2$$ elementos de $$A$$ tais que $$a_1
\neq a_2$$. Temos que $$g(f(a_1)) = a_1$$ e $$g(f(a_2)) = a_2$$, ou seja,
$$g(f(a_1)) \neq g(f(a_2))$$.

Se $$f(a_1)$$ fosse igual a $$f(a_2)$$, $$g$$ os enviaria para o mesmo
resultado. Mas o oposto disto deve ocorrer. Então $$f(a_1) \neq f(a_2)$$.

### Se $$f$$ é injetora, então $$f$$ tem inversa pela esquerda

Construiremos uma função $$g: B \rightarrow A$$ e mostraremos que ela é de fato
uma inversa de $$f$$ pela esquerda. Seja $$s$$ um elemento qualquer de $$A$$
($$A \neq \emptyset$$). Definamos então:

$$
g(b) =
\begin{cases}
    a \leftarrow f(a) = b, a \in A\\
    s \leftarrow b \notin \text{im}_f
\end{cases}
$$

Primeiramente vejamos por que $$g$$ é de fato uma função. Para qualquer $$b \in
B$$, ou $$b$$ é a imagem de algum $$a \in A$$ segundo $$f$$ ou não é. Em ambos
os casos nós temos um valor para $$g(b)$$ e assim varremos todo o conjunto
$$B$$. Se $$b$$ é tal que se adeque ao segundo caso ($$b \notin \text{im}_f$$),
o valor de $$g(b)$$ é sempre o mesmo, $$s$$. Caso contrário, pelo fato de $$f$$
ser injetora, não podem existir elementos distintos de $$A$$ que são mapeados em
$$b$$. Logo, $$a$$ é único e portanto $$g$$ é de fato uma função.

Agora vamos verificar se $$g$$ é de fato uma inversa de $$f$$ pela esquerda.
Segundo $$g$$, a imagem de um elemento $$y$$ tal que $$y$$ que é a imagem de um
elemento $$x$$ segundo $$f$$ é o próprio $$x$$. Logo $$g(f(x)) = x$$ e portanto
$$g \circ f$$ é a função identidade.

## Demonstração sugerida pelo autor

> Se a função $$f: A \rightarrow B$$ tem uma inversa pela direita e uma inversa
pela esquerda, então tais inversas são a mesma função.

Sejam $$g, h: B \rightarrow A$$ as inversas de $$f$$ pela esquerda e pela
direita, respectivamente. Mostraremos que $$\forall b \in B, g(b) = h(b)$$. Seja
então $$b$$ um elemento qualquer de $$B$$.

Como $$f$$ é sobrejetora (proposição 2.1.2), deve existir um elemento $$a \in
A$$ tal que $$b = f(a)$$. Já que $$g$$ é inversa à esquerda de $$f$$, $$g(b) =
g(f(a)) = a$$.

Como $$h$$ é inversa à direita de $$f$$, $$f(h(b)) = b = f(a)$$. Temos agora que
$$f(h(b)) = f(a)$$ e, como $$f$$ é injetora (proposição 2.1.1), $$h(b)$$ deve
ser igual a $$a$$.

Concluímos então que $$g(b) = a = h(b)$$.

## Proposição 2.3

> Uma função é injetora se, e somente se, ela é um monomorfismo.

### Se uma função é injetora, então ela é um monomorfismo

Sejam $$f: A \rightarrow B$$, $$Z$$ um conjunto e $$\mu, \nu: Z \rightarrow
A$$ tais que:

$$f \circ \mu = f \circ \nu$$

Pela proposição 2.1.1, seja $$g$$ a inversa à esquerda de $$f$$. Façamos a
composição pela esquerda e depois apliquemos a propriedade associativa:

$$g \circ (f \circ \mu) = g \circ (f \circ \nu)$$

$$(g \circ f) \circ \mu = (g \circ f) \circ \nu$$

$$\text{id}_A \circ \mu = \text{id}_A \circ \nu$$

$$\mu = \nu$$

### Se uma função é um monomorfismo, então ela é injetora

Seja $$f: A \rightarrow B$$ um monomorfismo. Suponhamos que $$f$$ não seja
injetora, ou seja, que existam $$a_1, a_2 \in A$$ tais que $$a_1 \neq a_2$$ e
$$f(a_1) = f(a_2)$$. Definamos então $$Z = \{a\} \subset A$$ e as funções $$\mu,
\nu: Z \rightarrow A$$ tais que $$\mu(a) = a_1$$ e $$\nu(a) = a_2$$.
Desenvolvemos então:

|$$(f \circ \mu)(a) = f(\mu(a)) = f(a_1)$$
|$$(f \circ \nu)(a) = f(\nu(a)) = f(a_2)$$
|

Como $$a$$ é o único elemento dos domínios de $$\mu$$ e $$\nu$$ e $$f(a_1) =
f(a_2)$$, temos que $$f \circ \mu = f \circ \nu$$ e portanto devemos esperar
que $$\mu$$ seja igual a $$\nu$$. No entanto, tais funções mapeiam o elemento
$$a$$ em valores diferentes $$a_1$$ e $$a_2$$ e, assim, são funções diferentes
entre si. Contradição.

## Demonstração sugerida pelo autor

> Se $$f$$ e $$\sim$$ são respectivamente uma função $$A \rightarrow B$$ e a
relação definida em $$\forall a', a'' \in A, a' \sim a''$$ $$\iff f(a') =
f(a'')$$, então $$\sim$$ é uma relação de quivalência.

1. $$\sim$$ é reflexiva: $$f(a)$$ é trivialmente igual a $$f(a)$$ e portanto $$a
\sim a$$.

2. $$\sim$$ é simétrica: sejam $$a_1, a_2 \in A$$ tais que $$a_1 \sim a_2$$.
Então $$f(a_1) = f(a_2)$$ e portanto $$a_2 \sim a_1$$.

3. $$\sim$$ é transitiva: sejam $$a_1, a_2, a_3 \in A$$ tais que $$a_1 \sim
a_2$$ e $$a_2 \sim a_3$$. Então $$f(a_1) = f(a_2)$$ e $$f(a_2) = f(a_3)$$. Logo,
$$f(a_1) = f(a_3)$$ e, assim, $$a_1 \sim a_3$$.

## Exercício 2.1

> Quantas bijeções distintas existem entre um conjunto $$S$$ com $$n$$ elementos
e ele próprio?

Selecionamos elementos de $$S$$ em uma ordem qualquer. Para cada elemento
selecionado, a quantidade de possibilidades para formar um novo par ordenado da
bijeção é igual a $$n$$ menos a quantidade de elementos selecionados
previamente. Portanto, a quantidade de bijeções distintas é igual a:

$$n \times (n-1) \times (n-2) \times \dots \times 1 = n!$$

## Exercício 2.2

> Prove a afirmação (2) da Proposição 2.1: $$f: A \rightarrow B$$ tem uma
inversa pela direita se e somente se $$f$$ for sobrejetora.

### Se $$f$$ tem inversa pela direita, então $$f$$ é sobrejetora

Se $$f$$ tem inversa pela direita, então existe $$g: B \rightarrow A$$ tal que
$$f(g(b)) = b$$ para todo $$b \in B$$.

Suponhamos que existe $$b^* \in B$$ tal que $$b^* \notin \text{im}_f$$. Para
$$b^*$$, não pode acontecer que $$f(g(b^*)) = b^*$$. Contradição.

### Se $$f$$ é sobrejetora, então $$f$$ tem inversa pela direita

Para cada elemento $$b \in B$$ definamos o conjunto $$A_b \subset A$$ composto
pelos elementos $$a \in A$$ tais que $$f(a) = b$$. Isto é possível porque $$f$$
é sobrejetora, então temos a garantia de que $$A_b$$ nunca é vazio.

Proposição: Para todos $$b_1, b_2 \in B$$ tais que $$b_1 \neq b_2$$ temos que
$$A_{b_1} \cap A_{b_2} = \emptyset$$.

Prova: Suponhamos que existe um $$a^* \in A_{b_1} \cap A_{b_2}$$. Como $$a^* \in
A_{b_1}$$, então $$f(a^*) = b_1$$. Como $$a^* \in A_{b_2}$$, então $$f(a^*) =
b_2$$. Contradição, pois $$f$$ é uma função.

Assim, podemos fazer uso do axioma da escolha para instanciar uma função $$h:
\{A_b | b \in B\} \rightarrow A$$ que seleciona um elemento fixo $$a_{b, h}$$ de
cada $$A_b$$. É importante ressaltar que $$f(a_{b, h}) = b$$, pois $$a_{b, h}
\in A_b$$. Agora podemos definir $$g: B \rightarrow A$$ segundo a lei de
formação:

$$g(b) = h(A_b) = a_{b, h}$$

Note que $$g$$ é uma função, pois:

* Está definida para todos os elementos de $$b \in B$$, já que $$A_b \neq
\emptyset$$;

* Leva cada elemento de $$B$$ em um único elemento de $$A$$, devido à construção
de $$h$$.

Agora só precisamos mostrar que $$g$$ é de fato uma inversa à direita de $$f$$.
Calculemos então $$(f \circ g)(b)$$:

$$(f \circ g)(b) = f(g(b)) = f(h(A_b)) = f(a_{b, h}) = b$$

Como $$b$$ é um elemento qualquer de $$B$$, $$f \circ g$$ é a própria função
identidade $$\text{id}_B$$.

## Exercício 2.3

> Prove que a inversa de uma bijeção é uma bijeção.

Sejam $$f: A \rightarrow B$$ uma função bijetora e $$g: B \rightarrow A$$ a sua
inversa. Se $$g$$ é a inversa de $$f$$, então $$g$$ é a inversa de $$f$$ pela
esquerda ($$g \circ f = \text{id}_A$$) e pela direita ($$f \circ g =
\text{id}_B$$). Mas notemos também as seguinte implicações:

* Se $$g \circ f = \text{id}_A$$ então $$f$$ é a inversa de $$g$$ pela direita

* Se $$f \circ g = \text{id}_B$$ então $$f$$ é a inversa de $$g$$ pela esquerda

Pelo Corolário 2.2, $$g$$ é bijetora pois tem uma inversa ($$f$$) pela direita e
pela esquerda.

> Prove que a composição de duas bijeções é uma bijeção.

Sejam $$f: A \rightarrow B$$ e $$g: B \rightarrow C$$ duas funções bijetoras e
$$h: A \rightarrow C$$ a composição $$g \circ f$$.

* $$h$$ é injetora: sejam $$a_1, a_2 \in A$$ tais que $$a_1 \neq a_2$$. Como
$$f$$ é injetora, temos que $$f(a_1) \neq f(a_2)$$. E como $$g$$ é injetora,
temos que $$g(f(a_1)) \neq g(f(a_2))$$.

* $$h$$ é sobrejetora: seja $$c \in C$$. Como $$g$$ é sobrejetora, existe $$b
\in B$$ tal que $$g(b) = c$$. Como $$f$$ é sobrejetora, existe $$a \in A$$ tal
que $$f(a) = b$$. Então $$c = g(b) = g(f(a)) = h(a)$$ e, portanto, $$c \in
\text{im}_h$$.

## Exercício 2.4

> Prove que *isomorfismo* é uma relação de equivalência.

Revisando o conceito de isomorfismo, dizemos que um conjunto $$A$$ é isomorfo a
um conjunto $$B$$, e denotamos esta relação por $$A \cong B$$, se, e somente se,
existe uma função bijetora de $$A$$ para $$B$$.

* Isomorfismo é uma relação reflexiva: Seja $$A$$ um conjunto qualquer.
*Proposição*: A função identidade $$\text{id}_A$$ é bijetora. *Prova*: A função
identidade é injetora porque para todos $$a_1, a_2 \in A$$ tais que $$a_1 \neq
a_2$$, $$\text{id}_A(a_1) \neq \text{id}_A(a_2)$$ (fazendo $$a_1 =
\text{id}_A(a_1)$$ e $$a_2 = \text{id}_A(a_2)$$). A função identidade
$$\text{id}_A$$ é sobrejetora porque todo elemento de $$A$$ é a imagem de um
elemento: ele próprio. Assim, $$A \cong A$$.

* Isomorfismo é uma relação simétrica: Sejam $$A$$ e $$B$$ conjuntos tais que
$$A \cong B$$ e $$f: A \rightarrow B$$ uma bijeção. Como demonstrado na questão
anterior, a função inversa $$f^{-1}: B \rightarrow A$$ é bijetora. Portanto, $$B
\cong A$$.

* Isomorfismo é uma relação transitiva: Sejam $$A$$, $$B$$ e $$C$$ conjuntos
tais que $$A \cong B$$ e $$B \cong C$$. Sejam também $$f: A \rightarrow B$$ e
$$g: B \rightarrow C$$ bijeções. Como demonstrado na questão anterior, a função
composta $$h: A \rightarrow C = g \circ f$$ é bijetora. Portanto $$A \cong C$$.

## Exercício 2.5

> Formule uma definição de epimorfismo no mesmo estilo da definição apresentada
para monomorfismo.

Uma função $$f: A \rightarrow B$$ é um epimorfismo se, para todos os conjuntos
$$Z$$ e todas as funções $$\mu, \nu: B \rightarrow Z$$:

$$\mu \circ f = \nu \circ f \implies \mu = \nu$$

> Mostre que uma função é sobrejetora se, e somente se, ela é um epimorfismo.

### Se uma função é sobrejetora, então ela é um epimorfismo

Sejam $$f: A \rightarrow B$$, $$Z$$ um conjunto qualquer e as funções $$\mu,
\nu: B \rightarrow Z$$ tais que:

$$\mu \circ f = \nu \circ f$$

Pela proposição 2.1.2, seja $$g$$ a inversa à direita de $$f$$. Façamos a
composição pela direita e depois apliquemos a propriedade associativa:

$$(\mu \circ f) \circ g = (\nu \circ f) \circ g$$

$$\mu \circ (f \circ g) = \nu \circ (f \circ g)$$

$$\mu \circ \text{id}_B = \nu \circ \text{id}_B$$

$$\mu = \nu$$

### Se uma função é um epimorfismo, então ela é sobrejetora

Seja $$f: A \rightarrow B$$ um epimorfismo. Suponhamos que $$f$$ não seja
sobrejetora, ou seja, $$\exists b \in B | b \notin \text{im}_f$$.

Definamos $$\mu, \nu: B \rightarrow \mathcal{P}(B)$$ de modo que:

$$\mu(b) = \{b\}$$

$$\nu(b) = \{b\} \cap \text{im}_f$$

Desenvolvendo $$(\mu \circ f)(a)$$ para todo $$a \in A$$:

$$(\mu \circ f)(a) = \mu(f(a)) = \{f(a)\}$$

Agora desenvolvendo $$(\nu \circ f)(a)$$ para todo $$a \in A$$:

$$(\nu \circ f)(a) = \nu(f(a)) = \{f(a)\} \cap \text{im}_f = \{f(a)\}$$

Como $$\mu \circ f = \nu \circ f$$ e $$f$$ é um epimorfismo, então $$\mu = \nu$$
e $$\mu(b) = \nu(b)$$.

Mas, substituindo, $$\{b\} = \{b\} \cap \text{im}_f$$ implica que $$b \in
\text{im}_f$$. Contradição.

## Exercício 2.6

> Explique como qualquer função $$f: A \rightarrow B$$ determina uma seção de
$$\pi_A$$.

Revisando o conceito de seção, uma seção é uma inversa à direita de uma função
sobrejetora. Primeiramente vamos mostrar que a projeção $$\pi_A: A \times B
\rightarrow A$$ é sobrejetora.

$$\pi_A$$ é sobrejetora porque todo elemento da sua imagem é definido
explicitamente como a primeira coordenada de algum elemento do produto
cartesiano $$A \times B$$.

Agora mostraremos que a seção de $$f$$, $$s_f: A \rightarrow A \times B$$, é uma
inversa à direita de $$\pi_A$$.

$$(\pi_A \circ s_f)(a) = \pi_A(s_f(a)) = \pi_A((a, f(a))) = a$$

Portanto $$\pi_A \circ s_f = \text{id}_A$$.

## Exercício 2.7

> Seja $$f: A \rightarrow B$$ uma função. Prove que o grafo $$\Gamma_f$$ de
$$f$$ é isomorfo a $$A$$.

Mostraremos que existe uma bijeção entre $$A$$ e $$\Gamma_f$$.

Seja $$g: A \rightarrow \Gamma_f$$ a função definida como $$g(a) = (a, f(a))$$.

$$g$$ é injetora pois dados $$a_1, a_2 \in A$$ com $$a_1 \neq a_2$$, temos que
$$g(a_1) = (a_1, f(a_1)) \neq (a_2, f(a_2)) = g(a_2)$$.

Suponhamos que $$g$$ não seja sobrejetora. Então existe $$(a^*, f(a^*)) \in
\Gamma_f$$ e que não pertence ao conjunto imagem de $$g$$. No entanto, $$a^* \in
A$$ e, como $$g$$ é uma função, $$a^*$$ tem imagem: $$g(a^*) = (a^*, f(a^*))$$.
Logo, $$(a^*, f(a^*)) \in \text{im}_g$$. Contradição.

## Exercício 2.8

> Explicite todos os termos da decomposição da função $$\mathbb{R} \rightarrow
\mathbb{C}$$ definida por $$f(x) = e^{2 \pi i x}$$.

Aplicando a fórmula de Euler: $$f(x) = \cos(2 \pi x) + i \sin(2 \pi x)$$. Se
observarmos os argumentos das funções trigonométricas, pelo fato deles serem
múltiplos de $$2\pi$$, constatamos que o valor de $$f(x)$$ é periódico, se
repetindo a cada inteiro.

Por isso podemos utilizar a relação de equivalência $$\sim$$ definida no
exercício 1.6 para colocarmos nas mesmas classes de equivalência todos os
elementos de $$\mathbb{R}$$ que possuem a mesma imagem segundo $$f$$.

Definamos então $$f_1: \mathbb{R} \rightarrow \mathbb{R}/\sim$$ da seguinte
forma:

$$f_1(x) := \{x^* \in \mathbb{R} | x - x^* \in \mathbb{Z}\}$$

Para a função seguinte, $$f_2: \mathbb{R}/\sim \rightarrow \mathbb{R}$$, faremos
uso do axioma da escolha para selecionarmos um representante de cada classe de
equivalência de forma determinística: o mais próximo de zero dentre seus
elementos não negativos.

$$f_2(X) := \text{arg min}_{x \in (X_{\geq 0})}(x)$$

E para o último passo definamos $$f_3: \mathbb{R} \rightarrow \mathbb{C}$$:

$$f_3(x) := e^{2 \pi i x}$$

Sendo $$f = f_1 \circ f_2 \circ f_3$$.

## Exercício 2.9

> Mostre que se $$A' \cong A''$$, $$B' \cong B''$$, $$A' \cap B' = \emptyset$$ e
$$A'' \cap B'' = \emptyset$$, então $$A' \cup B' \cong A'' \cup B''$$.

Sejam $$f_A: A' \rightarrow A''$$ e $$f_B: B' \rightarrow B''$$ bijeções, que
existem devido aos isomorfismos pressupostos.

Definamos $$g: A' \cup B' \rightarrow A'' \cup B''$$ como:

$$
g(n) =
\begin{cases}
f_A(n) \leftarrow n \in A'\\
f_B(n) \leftarrow n \in B'
\end{cases}
$$

Primeiramente, $$g$$ é uma função porque:

1. Todo elemento de $$A' \cup B'$$ é elemento de $$A'$$ ou de $$B'$$, portanto
todo elemento de $$A' \cup B'$$ tem uma imagem segunfo $$g$$;
2. Além disso, como $$A' \cap B' = \emptyset$$, a imagem de todo elemento de
$$A' \cup B'$$ segundo $$g$$ é única.

Agora mostraremos que $$g$$ é bijetora.

### $$g$$ é injetora

Sejam $$n_1, n_2 \in A' \cup B'$$ tais que $$n_1 \neq n_2$$.

* Se $$n_1, n_2 \in A'$$ então $$g(n_1) \neq g(n_2)$$ pois $$f_A(n_1) \neq
f_B(n_2)$$ já que $$f_A$$ é injetora;
* Se $$n_1, n_2 \in B'$$ segue que $$g(n_1) \neq g(n_2)$$ analogamente;
* Se $$n_1 \in A'$$ e $$n_2 \in B'$$, suponhamos que $$g(n_1) = g(n_2)$$, ou
seja, $$f_A(n_1) = f_B(n_2) = n^*$$. Como $$n^* \in A''$$ e $$n^* \in B''$$,
então $$n^* \in A'' \cap B''$$. Contradição;
* Se $$n_1 \in B'$$ e $$n_2 \in A'$$ segue que $$g(n_1) \neq g(n_2)$$
analogamente.

Em todo caso, $$g(n_1) \neq g(n_2)$$.

### $$g$$ é sobrejetora

Seja $$m \in A'' \cup B''$$. Mostraremos que $$m \in \text{im}_g$$.

* Se $$m \in A''$$, então $$m \in \text{im}_{f_A}$$ pois $$f_A$$ é sobrejetora e
portanto $$m \in \text{im}_g$$;
* Se $$m \in A''$$ segue que $$m \in \text{im}_g$$ analogamente.

Como $$A'' \cap B'' = \emptyset$$, temos que em todo caso $$m \in \text{im}_g$$.

> Conclua que $$A \amalg B$$ é bem definido segundo isomorfismo.

Mesmo sem entrarmos nos detalhes de como $$A'$$ e $$A''$$ foram criados a partir
de $$A$$ nem de como $$B'$$ e $$B''$$ foram criados a partir de $$B$$, ter que
$$A' \cap B' = \emptyset$$ e $$A'' \cap B'' = \emptyset$$, tal qual demanda a
definição de $$A \amalg B$$, foi suficiente para mostrar que as uniões
(disjuntas) de $$A'$$ com $$B'$$ e de $$A''$$ com $$B''$$ geram conjuntos
isomorfos entre si, ambos candidatos para $$A \amalg B$$.

## Exercício 2.10

> Mostre que se $$A$$ e $$B$$ são conjuntos finitos, então $$\vert B^A \vert =
\vert B \vert^{\vert A \vert}$$.

Faremos a demonstração por indução no tamanho de $$A$$. Como $$0^0$$ é
indeterminado, começaremos com o caso base $$\vert A \vert = 1$$.

Se $$A$$ é unitário, a quantidade de funções possíveis de serem construídas é
igual ao tamanho de $$B$$: uma função pra cada elemento de $$B$$. Então do lado
esquerdo temos que a quantidade de funções é $$\vert B \vert$$ e do lado direito
o resultado é $$\vert B \vert^1 = \vert B \vert$$.

Agora sejam $$n_A := \vert A \vert$$ e $$n_B := \vert B \vert$$ e suponhamos que
existam $${n_B}^{n_A}$$ funções de $$A$$ para $$B$$, ou seja, que a igualdade é
válida.

Seja $$A' = A \cup \{a\}$$, $$a \notin A$$. Então $$\vert A' \vert = n_A + 1$$.
Para cada função de $$A$$ para $$B$$ podemos criar $$n_B$$ novas funções de
$$A'$$ para $$B$$, pois $$a$$ pode estar relacionado com qualquer elemento de
$$B$$. Portanto a quantidade de funções de $$A'$$ para $$B$$, $$\vert B^{A'}
\vert$$, é igual a $${n_B}^{n_A} \times n_B = {n_B}^{n_A + 1} = {n_B}^{n_{A'}}
= \vert B \vert^{\vert A' \vert}$$.

## Exercício 2.11

> Mostre que existe uma bijeção entre $$2^A$$ e $$\mathcal{P}(A)$$, o conjunto
das partes de $$A$$.

Definamos $$g: 2^A \rightarrow \mathcal{P}(A)$$ como:

$$g(f) = \{a \in A| f(a) = 1\}, f: A \rightarrow \{0, 1\}$$

### $$g$$ é injetora

Sejam $$f_1, f_2 \in 2^A$$ tais que $$f_1 \neq f_2$$. Então existe $$a \in A$$
tal que $$f_1(a) \neq f_2(a)$$ de modo que apenas umas das possibilidades é
verdade:

* $$a \in g(f_1)$$ e $$a \notin g(f_2)$$
* $$a \notin g(f_1)$$ e $$a \in g(f_2)$$

Independentemente de qual for verdade, $$g(f_1) \neq g(f_2)$$.

### $$g$$ é sobrejetora

Sejam $$S \in \mathcal{P}(A)$$ e $$f_S \in 2^A$$ tais que:

$$
f_S(a) =
\begin{cases}
0 \leftarrow a \notin S\\
1 \leftarrow a \in S
\end{cases}
$$

Vamos calcular $$g(f_S)$$:

$$g(f_S) = \{a \in A | f_S(a) = 1\} = \{a \in A | a \in S\} = S$$

Portanto qualquer elemento de $$\mathcal{P}(A)$$ é imagem de algum elemento de
$$2^A$$.

