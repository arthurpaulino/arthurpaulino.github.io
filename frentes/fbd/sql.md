---
layout: page
title: SQL
---
# Um breve mergulho na semântica SQL

## Definindo os tipos

Consideremos os tipos fundamentais representados por `t`, onde `t` pode ser `int` ou `str`. Definamos então o tipo `coluna<t>` para que possamos construir o tipo `tabela< coluna1, coluna2, ... >`, que é o tipo básico da [SQL](https://pt.wikipedia.org/wiki/SQL){:target="_blank"}. Ou seja, o tipo `tabela` é composto por uma sequência de tipos `coluna`, cada um com seu próprio tipo fundamental.

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

O bloco para se executar uma consulta é formado pelas palavras chaves `select`, `from` e `where`, nesta ordem.

* `select` é sucedido por uma sequência de colunas `cols`
* `from` é sucedido por uma tabela `tab`
* `where` é sucedido por uma condição para a aceitação das linhas de `tab`

O resultado de uma consulta é uma tabela `result`, cujo tipo é `tabela<type_of(cols)>`.

Cada objeto da lista `cols` **deve** pertencer à sequência de colunas de `tab`.

Se a cláusula `where` for omitida, todas as linhas de `tab` farão parte de `result`.

* Exemplos:

	* A consulta

		~~~
		select empregados.nome
		from empregados
		where empregados.idade > 25
		~~~
	
		resulta na `tabela<[ coluna<str> ]>`

		| empregados.nome
		|:-:
		| zé
		| jó
	
	* A consulta

		~~~
		select empregados.nome
		from empregados
		~~~
	
		resulta na `tabela<[ coluna<str> ]>`

		| empregados.nome
		|:-:
		| zé
		| sá
		| jó
		| pi

### Variáveis

O escopo de uma consulta é definido na cláusula `from`. Desta forma, podemos instanciar variáveis para nos referirmos às tabelas.

* Exemplo:

	* A consulta

		~~~
		select e.nome
		from empregados e
		where e.idade = 25
		~~~

		resulta na `tabela<[ coluna<str> ]>`

		| e.nome
		|:-:
		| sá
		| pi

## Operações entre tabelas

### Produto cartesiano

Sintaxe: `<tabela> ← <tabela>, <tabela>`

Sejam as tabelas `A` do tipo `tabela< colunaA1, ... >` e `B` do tipo `tabela< colunaB1, ... >`. O produto cartesiano de `A` com `B` resulta em uma tabela do tipo `tabela< colunaA1, ..., colunaB1, ... >`.

* Exemplo:

	* A consulta
		
		~~~
		select *
		from departamentos d, campi c
		~~~
		
		resulta na `tabela< coluna<int>, coluna<str>, coluna<int>, coluna<int>, coluna<str> >`
		
		| d.id | d.nome | d.campus | c.id | c.nome
		|:-:|:-:|:-:|:-:|:-:
		| 1 | computação | 1 | 1 | pici
		| 1 | computação | 1 | 2 | benfica
		| 2 | biologia | 1 | 1 | pici
		| 2 | biologia | 1 | 2 | benfica
		| 3 | letras | 2 | 1 | pici
		| 3 | letras | 2 | 2 | benfica

À medida que encadeamos produtos cartesianos, o custo de memória aumenta muito rapidamente. Isto ocorre porque o produto cartesiano normalmente gera muitas linhas desinteressantes. Embora nós possamos filtrar as linhas que importam com a cláusula `where`, a memória do servidor já foi drasticamente consumida pelo [SGBD](https://pt.wikipedia.org/wiki/Sistema_de_gerenciamento_de_banco_de_dados){:target='_blank'}. Devido a este fato, uma boa prática é utilizar o

### Inner join

Sintaxe: `<tabela> ← <tabela> inner join <tabela> on <condição de emparelhamento>`

O `inner join` permite que filtremos as linhas de um produto cartesiano antes que elas passem a compor a tabela resultante.

A análise semântica é a mesma do produto cartesiano.

* Exemplo:

	* A consulta
		
		~~~
		select *
		from departamentos d inner join campi c on d.campus = c.id
		~~~
		
		resulta na `tabela< coluna<int>, coluna<str>, coluna<int>, coluna<int>, coluna<str> >`
		
		| d.id | d.nome | d.campus | c.id | c.nome
		|:-:|:-:|:-:|:-:|:-:
		| 1 | computação | 1 | 1 | pici
		| 2 | biologia | 1 | 1 | pici
		| 3 | letras | 2 | 2 | benfica

## Condições
