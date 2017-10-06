---
layout: page
title: SQL
---
# Um breve mergulho na semântica SQL

## Definindo os tipos

Consideremos os tipos fundamentais representados por `t`, onde `t` pode ser `int` ou `str`. Definamos então o tipo `coluna<t>` para que possamos construir o tipo `tabela< coluna1<t1>, coluna2<t2>, ... >`, que é o tipo básico da [SQL](https://pt.wikipedia.org/wiki/SQL){:target="_blank"}. Ou seja, o tipo `tabela` é composto por uma sequência de tipos `coluna`, cada um com seu próprio tipo fundamental `t`.

* Exemplos:

	* Seja `campi` a `tabela< coluna<int>, coluna<str> >`

		| campi.id | campi.nome
		|:-:|:-:
		| 1 | pici
		| 2 | benfica

	* Seja `departamentos` a `tabela< coluna<int>, coluna<str>, coluna<int> >`

		| departamentos.id | departamentos.nome | departamentos.campus
		|:-:|:-:|:-:
		| 1 | computação | 1
		| 2 | biologia | 1
		| 3 | letras | 2

	* Seja `empregados` a `tabela< coluna<int>, coluna<str>, coluna<int>, coluna<int> >`

		| empregados.id | empregados.nome | empregados.idade | empregados.departamento
		|:-:|:-:|:-:|:-:
		| 1 | zé | 26 | 3
		| 2 | sá | 25 | 2
		| 3 | jó | 27 | 1
		| 4 | pi | 25 | 1

## Consultas

O bloco para se executar uma consulta é formado pelas palavras chaves **`select`**, **`from`** e **`where`**, nesta ordem.

* **`select`** é sucedido por uma sequência de colunas `cols`
* **`from`** é sucedido por uma tabela `tab`
* **`where`** é sucedido por uma condição para a aceitação das linhas de `tab`

O resultado de uma consulta é uma tabela `result`, cujo tipo é `tabela<type_of(cols)>`.

Cada objeto da lista `cols` **deve** pertencer à sequência de colunas de `tab`.

Se a cláusula **`where`** for omitida, todas as linhas de `tab` farão parte de `result`.

* Exemplos:

	* A consulta

		~~~ sql
		select empregados.nome
		from empregados
		where empregados.idade > 25
		~~~
	
		resulta na seguinte `tabela<[ coluna<str> ]>`

		| empregados.nome
		|:-:
		| zé
		| jó
	
	* A consulta

		~~~ sql
		select empregados.nome
		from empregados
		~~~
	
		resulta na seguinte `tabela<[ coluna<str> ]>`

		| empregados.nome
		|:-:
		| zé
		| sá
		| jó
		| pi

### Variáveis

O escopo de uma consulta é definido na cláusula **`from`**. Desta forma, podemos instanciar variáveis para nos referirmos às tabelas.

* Exemplo:

	* A consulta

		~~~ sql
		select e.nome
		from empregados e
		where e.idade = 25
		~~~

		resulta na seguinte `tabela<[ coluna<str> ]>`

		| e.nome
		|:-:
		| sá
		| pi
