---
layout: post
title: Área Abaixo da Curva ROC
subtitle: Em busca de uma intuição
tags:
  - data-science
  - metrics
  - roc-auc-score
---

Em todas as competições do [Kaggle](https://www.kaggle.com/){:target="\_blank"}
que eu participei e que envolviam classificações binárias, a métrica de avaliação
foi a Área Abaixo da Curva ROC (**AUC**). Por conta disso, eu fui procurar por uma
explicação para essa métrica.

Um dos melhores links que eu encontrei foi [esse](https://www.dataschool.io/roc-curves-and-auc-explained/){:target="\_blank"},
que contém ilustrações que facilitam a compreensão. Mas eu ainda não estava satisfeito,
pois o assunto ainda não tinha chegado na minha intuição com clareza.

Eu continuei buscando e então me deparei com esta resposta no
[StackExchange](https://stats.stackexchange.com/a/133435){:target="\_blank"}:

> A **AUC** de um classificador é a probabilidade de que um exemplo positivo
aleatório seja pontuado acima de um exemplo negativo aleatório.

Bingo! Finalmente uma explicação que chegou à minha compreensão. Mas e aí, por que
isso é verdade? Eu busquei várias explicações para esse fato mas não consegui entender
direito com nenhuma delas isoladamente. Portanto, decidi escrever este texto após
mastigar bastante sobre o assunto.

Vamos então definir matematicamente a **AUC**. Seja $$f$$ a função do classificador,
que recebe uma entrada $$x$$ e retorna a probabilidade $$f(x)$$ de $$x$$ ser um
caso positivo. Ao definirmos um valor $$T$$ para que o classificador responda
**sim** quando $$f(x) > T$$ ou **não** quando $$f(x) < T$$, normalmente cometemos
erros acusando falsos positivos e falsos negativos. A taxa de verdadeiros positivos
($$TPR$$) é a razão entre a quantidade de casos positivos para os quais o classificador
disse **sim** e a quantidade de casos positivos. A taxa de falsos positivos ($$FPR$$)
é a razão entre a quantidade de casos negativos para os quais o classificador disse
**sim** e a quantidade de casos negativos. Assim, a curva ROC é definida pelos
pontos $$(FPR, TPR)$$, onde $$T \in (-\infty, \infty)$$. A **AUC** está ilustrada
na Figura 1.

![](/assets\img\2018-10-06-0.png){:class="img-responsive"}
*Figura 1*

Formalmente, consideramos $$TPR$$ como uma função de $$FPR$$ e integramos de 0 a
1 para calcularmos a área:

$$\textrm{AUC} = \int_0^1 TPR(FPR) dFPR \hspace{1cm}(1)$$

No entanto, $$TPR$$ e $$FPR$$ são funções de $$T$$. Sendo $$FPR'$$ a derivada de
$$FPR(T)$$ em relação a $$T$$, temos que $$dFPR = FPR'(T)dT$$. Antes de fazermos
a [substituição de variável na integral](https://en.wikipedia.org/wiki/Integration_by_substitution){:target="\_blank"},
note que:

- $$FPR(\infty) = 0$$, pois nenhum caso é classificado como positivo
- $$FPR(-\infty) = 1$$, pois todos os casos são classificados como positivos

Substituindo na Equação 1, obtemos:

$$\textrm{AUC} = \int_{\infty}^{-\infty} TPR(FPR(T)) FPR'(T) dT$$

Seja $$x^+$$ uma variável aleatória discreta que assume valores dentre os casos
positivos com distribuição uniforme. Denotemos por $$f(x^+)$$ a variável aleatória
contínua resultante da aplicação da função $$f$$ em cada caso positivo $$x^+$$.
A taxa de verdadeiros positivos pode ser entendida como a probabilidade de que
$$f(x^+)$$ seja maior que $$T$$. Além disso, trocando os limites da integral e
invertendo o sinal do integrando, obtemos:

$$\textrm{AUC} = \int_{-\infty}^{\infty} P(f(x^+) > T) [-FPR'(T)] dT$$

Substituindo $$[-FPR'(T)]$$ pela derivada de uma primitiva estratégica:

$$\textrm{AUC} = \int_{-\infty}^{\infty} P(f(x^+) > T) \left[ \frac{d}{dT}(1 - FPR(T)) \right] dT$$

Complementar à taxa de falsos positivos, temos a taxa de verdadeiros negativos
($$TNR$$), que é a razão entre a quantidade de casos negativos para os quais o
modelo respondeu não e a quantidade de casos negativos. Assim, $$TNR(T) = 1-FPR(T)$$:

$$\textrm{AUC} = \int_{-\infty}^{\infty} P(f(x^+) > T) TNR'(T) dT \hspace{1cm}(2)$$
