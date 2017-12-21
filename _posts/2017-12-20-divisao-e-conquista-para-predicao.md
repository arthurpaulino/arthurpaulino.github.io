---
layout: post
title: Divisão e conquista para predição
tags:
  - data-science
  - machine-learning
  - k-means
---

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

Nem sempre é possível encontrar um único modelo que prediz qualquer entrada de maneira confiável. Nestes casos, uma estratégia possível é dividir o espaço amostral para encontrarmos **alguns** clusters nos quais nossos modelos de aprendizado são capazes de obter resultados mais acurados.

Neste artigo apresentarei uma forma de implementar a divisão e conquista utilizando o algoritmo $$k$$-means. Mas antes, façamos uma breve revisão.

$$k$$-means é um algoritmo de *clusterização*, ou seja, sua utilidade é agrupar elementos semelhantes.
