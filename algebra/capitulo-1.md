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

Acontece que (1) não pode ser verdade, pois, pela própria definição, $$R$$ não é
composto por conjuntos que pertençam a si próprios.

Então (2) deve ser verdade? Ora, se $$R$$ não pertence a si próprio, então, pela
definição de $$R$$, ele deveria pertencer a si próprio, pois $$R$$ é composto
por **todos** os conjuntos que não têm a si próprios como elementos.
Contradição!

Assim, conjunto definido de tal maneira não pode existir.

## Exercício 1.2

> Prove that if $$∼$$ is an equivalence relation on a set $$S$$, then the
corresponding family $$\mathscr{P}_∼$$ defined in §1.5 is indeed a partition of
$$S$$: that is, its elements are nonempty, disjoint and their union is $$S$$.
