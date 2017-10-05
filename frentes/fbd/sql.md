---
layout: page
title: SQL
---
# Um breve mergulho na semântica SQL

## Definindo os tipos

Consideremos os tipos fundamentais representados por `t`, onde `t` pode ser `int` ou `str`. Definamos então o tipo `coluna<[:t:]>`, uma lista (`[]`) de objetos do tipo `t`, para que possamos construir o tipo `tabela<[:coluna:]>`, que é o tipo básico da [SQL](https://pt.wikipedia.org/wiki/SQL){:target="_blank"}. Ou seja, uma `tabela` é formada por uma lista de objetos do tipo `coluna`, cada um com seu próprio tipo fundamental.

***

Exemplo:

Seja **empregados** a `tabela<[ coluna<[:int:]>, coluna<[:str:]>, coluna<[:int:]>, coluna<[:str:]> ]>`

| empregados.id | empregados.nome | empregados.idade | empregados.departamento
|:-:|:-:|:-:|:-:
| 1 | zé | 26 | computação
| 2 | sá | 25 | biologia
| 3 | jó | 27 | matemática

## Consultas

O bloco para se executar uma consulta é formado pelas palavras chaves `select`, `from` e `where`, nesta ordem.

* `select` é sucedido de uma lista de colunas `cols`
* `from` é sucedido de uma `tabela` `tab`
* `where` é sucedido de uma condição para a aceitação dos elementos das colunas de `tab`

A cláusula `where` é opcional e cada objeto da lista `cols` *deve* pertencer à lista de colunas de `tab`. O resultado de uma consulta é um objeto do tipo `tabela`.

***

Exemplo:
~~~
select empregados.nome, empregados.departamento
from empregados
where empregados.idade > 25
~~~
resultará na seguinte `tabela<[coluna<[:str:]>, coluna<[:str:]>]>`

| empregados.nome | empregados.departamento
|:-:|:-:
| zé | computação
| jó | matemática
