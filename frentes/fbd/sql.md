---
layout: page
title: SQL
---
# Um breve mergulho na semântica SQL

## Definindo os tipos

Consideremos os tipos fundamentais representados por `t`, onde `t` pode ser `int` ou `str`. Definamos então o tipo `coluna<t>` para que possamos construir o tipo `tabela<[:coluna:]>`, que é o tipo básico da [SQL](https://pt.wikipedia.org/wiki/SQL){:target="_blank"}. Ou seja, uma tabela é formada por uma lista de objetos do tipo `coluna`, cada um com seu próprio tipo fundamental.

* Exemplos:

	* Seja `campi` a `tabela<[ coluna<int>, coluna<str> ]>`

		| campi.id | campi.nome
		|:-:|:-:
		| 1 | pici
		| 2 | benfica

	* Seja `departamentos` a `tabela<[ coluna<int>, coluna<str>, coluna<int> ]>`

		| departamentos.id | departamentos.nome | departamentos.campus
		|:-:|:-:|:-:
		| 1 | computação | 1
		| 2 | biologia | 1
		| 3 | letras | 2

	* Seja `empregados` a `tabela<[ coluna<int>, coluna<str>, coluna<int>, coluna<int> ]>`

		| empregados.id | empregados.nome | empregados.idade | empregados.departamento
		|:-:|:-:|:-:|:-:
		| 1 | zé | 26 | 3
		| 2 | sá | 25 | 2
		| 3 | jó | 27 | 1
		| 4 | pi | 25 | 1

## Consultas

O bloco para se executar uma consulta é formado pelas palavras chaves **`select`**, **`from`** e **`where`**, nesta ordem.

* **`select`** é sucedido por uma lista de colunas `cols`
* **`from`** é sucedido por uma `tabela` `tab`
* **`where`** é sucedido por uma condição para a aceitação das linhas de `tab`

A cláusula **`where`** é opcional e cada objeto da lista `cols` *deve* pertencer à lista de colunas de `tab`. O resultado de uma consulta é um objeto do tipo `tabela<cols>`.

* Exemplo:

	~~~ sql
	select empregados.nome
	from empregados
	where empregados.idade > 25
	~~~
	resultará na seguinte `tabela<[ coluna<str> ]>`

	| empregados.nome
	|:-:
	| zé
	| jó

### Variáveis

O escopo de uma consulta é definido na cláusula **`from`**. Desta forma, podemos instanciar variáveis para nos referirmos às tabelas.

* Exemplo:

	~~~ sql
	select e.nome
	from empregados e
	where e.idade = 25
	~~~

	resultará na seguinte `tabela<[ coluna<str> ]>`

	| e.nome
	|:-:
	| sá
	| pi
