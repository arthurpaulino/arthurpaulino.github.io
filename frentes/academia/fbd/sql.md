---
layout: page
title: SQL
---
# Um breve mergulho na semântica SQL

## Definindo os tipos

Consideremos os tipos fundamentais representados por `t`, onde `t` pode ser `num` ou `str`. Definamos então o tipo `coluna<t>` para que possamos construir o tipo `tabela< coluna<t1>, coluna<t2>, ... >`, que é o tipo básico da [SQL](https://pt.wikipedia.org/wiki/SQL){:target="_blank"}. Ou seja, o tipo `tabela` é composto por uma sequência de tipos `coluna`, cada um com seu próprio tipo fundamental.

* Exemplos:

	* Seja `campi` a `tabela< coluna<num>, coluna<str> >`

		| campi.id | campi.nome
		|:-:|:-:
		| 1 | pici
		| 2 | benfica
		| 3 | porangabussu

	* Seja `departamentos` a `tabela< coluna<num>, coluna<str>, coluna<num> >`

		| departamentos.id | departamentos.nome | departamentos.campus
		|:-:|:-:|:-:
		| 1 | computação | 1
		| 2 | biologia | 1
		| 3 | letras | 2

	* Seja `empregados` a `tabela< coluna<num>, coluna<str>, coluna<num>, coluna<num> >`

		| empregados.id | empregados.nome | empregados.idade | empregados.salário | empregados.departamento
		|:-:|:-:|:-:|:-:|:-:
		| 1 | zé | 26 | 900 | 3
		| 2 | sá | 25 | 925 | 2
		| 3 | jó | 27 | 950 | 1
		| 4 | pi | 25 | 975 | 1

## Consultas

O bloco para se executar uma consulta é formado pelas palavras chaves `select`, `from` e `where`, nesta ordem.

* `select` é sucedido por uma sequência de colunas `cols`
* `from` é sucedido por uma tabela `tab`
* `where` é sucedido por uma condição para a aceitação das linhas de `tab`

O resultado de uma consulta é uma tabela `result`, cujo tipo é `tabela< type(cols[0]), type(cols[1]), ... >`.

Cada objeto da lista `cols` **deve** pertencer à sequência de colunas de `tab`. O caractere `*` representa uma lista de colunas que contem todas as colunas de `tab`.

Se a cláusula `where` for omitida, todas as linhas de `tab` farão parte de `result`.

* Exemplos:

	* A consulta

		~~~
		select empregados.nome
		from empregados
		where empregados.idade > 25
		~~~
	
		resulta na `tabela< coluna<str> >`

		| empregados.nome
		|:-:
		| zé
		| jó
	
	* A consulta

		~~~
		select empregados.nome
		from empregados
		~~~
	
		resulta na `tabela< coluna<str> >`

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

		resulta na `tabela< coluna<str> >`

		| e.nome
		|:-:
		| sá
		| pi

## Operações entre tabelas

### Produto cartesiano

Sintaxe: `<tabela>, <tabela>` → `<tabela>`

Sejam as tabelas `A` do tipo `tabela< colunaA1, ... >` e `B` do tipo `tabela< colunaB1, ... >`. O produto cartesiano de `A` com `B` resulta em uma tabela do tipo `tabela< colunaA1, ..., colunaB1, ... >`.

* Exemplo:

	* A consulta
		
		~~~
		select *
		from departamentos d, campi c
		~~~
		
		resulta na `tabela< coluna<num>, coluna<str>, coluna<num>, coluna<num>, coluna<str> >`
		
		| d.id | d.nome | d.campus | c.id | c.nome
		|:-:|:-:|:-:|:-:|:-:
		| 1 | computação | 1 | 1 | pici
		| 1 | computação | 1 | 2 | benfica
		| 1 | computação | 1 | 3 | porangabussu
		| 2 | biologia | 1 | 1 | pici
		| 2 | biologia | 1 | 2 | benfica
		| 2 | biologia | 1 | 3 | porangabussu
		| 3 | letras | 2 | 1 | pici
		| 3 | letras | 2 | 2 | benfica
		| 3 | letras | 2 | 3 | porangabussu

À medida que encadeamos produtos cartesianos, o custo de memória aumenta muito rapidamente. Isto ocorre porque o produto cartesiano normalmente gera muitas linhas desinteressantes. Embora nós possamos filtrar as linhas que importam com a cláusula `where`, a memória do servidor já foi drasticamente consumida pelo [SGBD](https://pt.wikipedia.org/wiki/Sistema_de_gerenciamento_de_banco_de_dados){:target='_blank'}. Devido a este fato, uma boa prática é utilizar o

### `inner join`

Sintaxe: `<tabela> inner join <tabela> on <condição de emparelhamento>` → `<tabela>`

O `inner join` permite que filtremos as linhas de um produto cartesiano antes que elas passem a compor a tabela resultante.

A análise semântica é a mesma do produto cartesiano.

* Exemplo:

	* A consulta
		
		~~~
		select *
		from departamentos d inner join campi c on d.campus = c.id
		~~~
		
		resulta na `tabela< coluna<num>, coluna<str>, coluna<num>, coluna<num>, coluna<str> >`
		
		| d.id | d.nome | d.campus | c.id | c.nome
		|:-:|:-:|:-:|:-:|:-:
		| 1 | computação | 1 | 1 | pici
		| 2 | biologia | 1 | 1 | pici
		| 3 | letras | 2 | 2 | benfica

### `left join` e `right join`

Se quisermos que a tabela resultante contenha todas as linhas de uma das tabelas do `join` mesmo que não haja correspondência para satisfazer a condição de emparelhamento, utilizamos `left join` ou `right join`. As células sem elementos correspondentes são preenchidas com objetos nulos.

Sintaxes e análises semânticas análogas ao `inner join`.

* Exemplos:

	* A consulta
		
		~~~
		select *
		from campi c left join departamentos d on d.campus = c.id
		~~~
		
		resulta na `tabela< coluna<num>, coluna<str>, coluna<num>, coluna<str>, coluna<num> >`
		
		| c.id | c.nome | d.id | d.nome | d.campus
		|:-:|:-:|:-:|:-:|:-:
		| 1 | pici | 1 | computação | 1
		| 1 | pici | 2 | biologia | 1
		| 2 | benfica | 3 | letras | 2
		| 3 | porangabussu |  |  | 
	
	* A consulta
		
		~~~
		select *
		from departamentos d right join campi c on d.campus = c.id
		~~~
		
		resulta na `tabela< coluna<num>, coluna<str>, coluna<num>, coluna<num>, coluna<str> >`
		
		| d.id | d.nome | d.campus | c.id | c.nome
		|:-:|:-:|:-:|:-:|:-:
		| 1 | computação | 1 | 1 | pici
		| 2 | biologia | 1 | 1 | pici
		| 3 | letras | 2 | 2 | benfica
		|  |  |  | 3 | porangabussu

### `union`

Sintaxe: `<tabela> union <tabela>` → `<tabela>`

O operador `union` requer que as tabelas fornecidas sejam do mesmo tipo, ou seja
* Suas sequências de colunas devem ter o mesmo tamanho
* Suas sequências de colunas devem ter colunas do mesmo tipo em cada posição das sequências

Os nomes das colunas da tabela resultante são os nomes das colunas da primeira tabela.

* Exemplos:

	* A consulta

		~~~
		select empregados.nome, empregados.salário
		from empregados
		union
		select departamentos.nome, departamentos.campus
		from departamentos
		~~~
	
		resulta na `tabela< coluna<str>, coluna<num> >` **sem consistência interpretativa**

		| empregados.nome | empregados.salário
		|:-:|:-:
		| zé | 900
		| sá | 925
		| jó | 950
		| pi | 975
		| computação | 1
		| biologia | 1
		| letras | 2
	
	* A consulta
		
		~~~
		select *
		from (
			select c.id, c.nome
			from campi c
			union
			select d.id, d.nome
			from departamentos d
			union
			select e.id, e.nome
			from empregados e
		) dados
		~~~
		
		resulta na `tabela< coluna<num>, coluna<str> >`
		
		| dados.id | dados.nome
		|:-:|:-:
		| 1 | pici
		| 2 | benfica
		| 3 | porangabussu
		| 1 | computação
		| 2 | biologia
		| 3 | letras
		| 1 | zé
		| 2 | sá
		| 3 | jó
		| 4 | pi

## Condições

### `=`, `<>` ou`!=`, `>`, `>=`, `<` e `<=`

Operadores utilizados para fazermos comparações entre objetos do mesmo tipo básico. No tipo `str`, a magnitude considerada é a ordem alfabética.

### `in`

Retorna `true` se um objeto pertence à lista em questão.

* Exemplo:

	* A consulta

		~~~
		select e.nome
		from empregados e inner join departamentos d on e.departamento = d.id
		where d.departamento in ('computação', 'letras')
		~~~
	
		resulta na `tabela< coluna<str> >`

		| e.nome
		|:-:
		| sá
		| jó
		| pi

Se uma `<tabela>` possui apenas uma coluna, ela pode ser utilizada como uma lista.

* Exemplo:

	* A consulta

		~~~
		select departamentos.nome
		from departamentos
		where departamentos.id in (
			select empregados.departamento
			from empregados
			where empregados.salário < 950
		)
		~~~
	
		resulta na `tabela< coluna<str> >`

		| departamentos.nome
		|:-:
		| biologia
		| letras

A negação de `in` é `not in`.

## Funções de agregação

Para melhorar a legibilidade das consultas que incluem funções de agregação, nós daremos nomes fictícios às colunas resultantes com o auxílio da palavra-chave `as`.

### `count`

Computa a quantidade de objetos não nulos da coluna escolhida. Um cuidado extra é requerido para usar `count` em tabelas provenientes de `left join` ou `right join`.

* Exemplos:

	* A consulta

		~~~
		select count(empregados.id) as quantidade
		from empregados
		where empregados.salário > 900
		~~~
	
		resulta na `tabela< coluna<num> >` **de nome indeterminado**

		| quantidade
		|:-:
		| 3
	
	* A consulta

		~~~
		select *
		from (
			select count(empregados.id) as quantidade
			from empregados
			where empregados.salário > 900
		) resultado
		
		~~~
	
		resulta na `tabela< coluna<num> >` **cujo nome é `resultado`**

		| resultado.quantidade
		|:-:
		| 3

Caso não importe se a tabela tenha ou não objetos nulos, podemos utilizar `count(*)`.

* Exemplo:

	* A consulta

		~~~
		select *
		from (
			select count(*) as quantidade
			from empregados
			where empregados.salário > 900
		) resultado
		
		~~~
	
		resulta na `tabela< coluna<num> >`

		| resultado.quantidade
		|:-:
		| 3

### `min` e `max`

Computam respectivamente o mínimo e o máximo valor de uma coluna. Em colunas cujo tipo básico é `str`, a magnitude considerada é a ordem alfabética.

### `sum` e `avg`

Funções utilizadas exclusivamente em colunas cujo tipo básico é `num`. Elas computam respectivamente a soma e a média dos valores da coluna.

### `group by`

As funções de agregação normalmente são utilizadas para gerar tabelas com apenas uma linha.

* Exemplo:
	
	* A consulta

		~~~
		select *
		from (
			select count(*) as quantidade, min(e.salário) as min_sal, max(e.salário) as max_sal,
				sum(e.salário) as sum_sal, avg(e.salário) as avg_sal
			from empregados e
		) resultado
		
		~~~
	
		resulta na `tabela< coluna<num>, coluna<num>, coluna<num>, coluna<num>, coluna<num> >`

		| resultado.quantidade | resultado.min_sal | resultado.max_sal | resultado.sum_sal | resultado.avg_sal
		|:-:|:-:|:-:|:-:|:-:
		| 3 | 900 | 975 | 3750 | 937.5

Mas nós podemos utilizar `group by` para que os resultados das funções de agregação sejam computados em blocos isolados. Para isto, à exceção da coluna elegida para o `group by`, todas as outras colunas mencionadas na cláusula `select` devem gerar **apenas uma linha**, como é o caso das funções de agregação.

* Exemplo:
	
	* A consulta

		~~~
		select *
		from (
			select e.departamento, count(*) as quantidade, min(e.salário) as min_sal,
				max(e.salário) as max_sal, sum(e.salário) as sum_sal, avg(e.salário) as avg_sal
			from empregados e
			group by e.departamento
		) resultado
		
		~~~
	
		|resulta na
		|`tabela< coluna<num>, coluna<num>, coluna<num>, coluna<num>, coluna<num>, coluna<num> >`

		| resultado.departamento | resultado.quantidade | resultado.min_sal | resultado.max_sal | resultado.sum_sal | resultado.avg_sal
		|:-:|:-:|:-:|:-:|:-:|:-:
		| 3 | 1 | 900 | 900 | 900 | 900
		| 2 | 1 | 925 | 925 | 925 | 925
		| 1 | 2 | 950 | 975 | 1925 | 962.5

## Links recomendados
* [w3schools](https://www.w3schools.com/sql/){:target="_blank"}
* [Wikipédia](https://pt.wikipedia.org/wiki/SQL){:target="_blank"}
