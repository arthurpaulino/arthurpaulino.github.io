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

    Agora suponhamos que existe um elemento, $$s \in S$$ que não pertence a
    $$U$$. Por reflexividade, temos que $$s \sim s$$. Assim sendo, existe a
    classe de equivalência $$[s]_\sim$$ composta por, pelo menos, o elemento
    $$s$$. Ao realizarmos a operação de união entre todas as classes de
    equivalência de $$S$$ para computarmos $$U$$, o elemento $$s$$ pertencerá a
    $$U$$. Contradição
