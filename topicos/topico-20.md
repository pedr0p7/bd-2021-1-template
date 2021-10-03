## [Tópico T20] - SQL - DML (Data Manipulation Language): Subconsulta (parte 1)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

Os exemplos apresentados usam o esquema lógico do **BD Empresa**, conforme abaixo.

<img src="../media/fig-esquema-logico-bdempresa.jpg" width="450">

### Subconsulta

Uma subconsulta consiste em um comando SELECT posicionado dentro de um outro comando SQL. Com maior frequência, subconsultas estão inseridas em outras consultas, ou seja, consultas aninhadas:
- A subconsulta é denominada _consulta interna_.
- A consulta na qual a subconsulta está embutida é chamada _consulta externa_.
- A subconsulta usualmente está localizada na cláusula WHERE, na cláusula FROM e/ou na cláusula SELECT, conforme necessário.

Um classificação comum para subconsultas é:
- **Subconsulta Independente**: a execução da subconsulta é independente da consulta mais externa:
  - a subconsulta é executada uma única vez;
  - o resultado da subconsulta é utilizado para o processamento da consulta mais externa.
- **Subconsulta Corretata**: a execução da subconsulta é dependente da consulta mais externa:
  - a subconsulta é potencialmente executada várias vezes:
    - a subconsulta é avaliada uma vez para cada _tupla_ (ou combinação de _tuplas_) na consulta externa.
  - a subconsulta requer dados oriundos da consulta externa para ser processada.

### Cláusula IN

A Cláusula **IN** é similar à operação de conjuntos "se pertence":<br>
■ Por exemplo, "_o elemento **a** pertence ao conjunto **C**?_" Ou seja, "**a ∈ C**?"

### Exemplo 01: Cláusula IN
#### Qual o nome dos funcionários que possuem o menor salário na empresa?

|Classificação|SQL|
|-|-|
|Subconsulta independente|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Salario IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT MIN(Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )<br><br>SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Salario = (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT MIN(Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )|

### Exemplo 02: Cláusula IN
#### Qual o nome dos funcionários que são gerentes de departamento?

|Classificação|SQL|
|-|-|
|Subconsulta independente|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Cpf IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Cpf_gerente**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPARTAMENTO** )<br><br>**_# Comando abaixo está correto?_**<br>SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Cpf = (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Cpf_gerente**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPARTAMENTO** )|

### Exemplo 03: Cláusula NOT IN
#### Qual o nome dos funcionários que não possuem o menor salário nem o maior salário?

|Classificação|SQL|
|-|-|
|Subconsulta independente|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Salario NOT IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT MIN(Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )<br>AND&nbsp;&nbsp;&nbsp;Salario NOT IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT MAX(Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )<br><br>SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Salario > (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT MIN(Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )<br>AND&nbsp;&nbsp;&nbsp;Salario < (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT MAX(Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )|

### Exemplo 04: Cláusula NOT IN
#### Qual o nome dos funcionários que trabalham 10 horas em algum projeto?

|Classificação|SQL|
|-|-|
|Subconsulta independente|**_# A consulta abaixo deveria retornar tuplas iguais?_**<br>SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE (Cpf, 10) IN<br>&nbsp;&nbsp;&nbsp;&nbsp;( **SELECT Fcpf, Horas**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**FROM TRABALHA_EM** )|

### Cláusula EXISTS

A cláusula (função?) EXISTS é utilizada para verificar se o resultado de uma subconsulta retorna alguma _tupla_:<br>
&#9888; **True**, se a subconsulta retornar uma ou mais _tuplas_;<br>
&#9888; **False**, se a subconsulta não retornar qualquer _tupla_.

A Cláusula EXISTS é usualmente aplicada em subconsultas correlatas.

### Exemplo 05: EXISTS
#### Qual o nome dos funcionários que "possuem dependentes"?

|Classificação|SQL|
|-|-|
|Subconsulta correlata|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT \***<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPENDENTE**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE FUNCIONARIO.Cpf = DEPENDENTE.Fcpf** )<br><br>SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT NULL**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPENDENTE**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE FUNCIONARIO.Cpf = DEPENDENTE.Fcpf** )|

### Exemplo 06: EXISTS
#### Qual o nome dos funcionários que "não possuem dependentes"?

|Classificação|SQL|
|-|-|
|Subconsulta correlata|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE NOT EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT \***<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPENDENTE**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE FUNCIONARIO.Cpf = DEPENDENTE.Fcpf** )<br><br>SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE NOT EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT 1**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPENDENTE**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE FUNCIONARIO.Cpf = DEPENDENTE.Fcpf** )|

### Exemplo 07: EXISTS e Operadores '<' e '>'
#### Qual o nome e salário dos funcionários que "não têm o maior salário na empresa"?

|Classificação|SQL|
|-|-|
|Subconsulta correlata|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT \***<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE INTERNA.Salario > EXTERNA.Salario** )|

#### Qual o nome e salário dos funcionários que "têm o menor salário na empresa"?

|Classificação|SQL|
|-|-|
|Subconsulta correlata|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE NOT EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT \***<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE INTERNA.Salario < EXTERNA.Salario** )|

### Exemplo 08: Operadores '<' e '>' e Funções Agregadas
#### Qual o nome e salário dos funcionários que "estão entre os três maiores salários da empresa"?

|Classificação|SQL|
|-|-|
|Subconsulta correlata|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE 3 > (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT COUNT(DISTINCT Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE INTERNA.Salario > EXTERNA.Salario** )|

#### Qual o nome e salário dos funcionários que "estão entre os dois menores salários da empresa"?

|Classificação|SQL|
|-|-|
|Subconsulta correlata|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE 3 < (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT COUNT(DISTINCT Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE INTERNA.Salario > EXTERNA.Salario** )|

## Atividade (data limite: **xx/xx/xxxx 23h59min59s**)

Criar uma _issue_ no projeto https://github.com/plinioleitao/bd-2021-1-bxx, com o título "Tópico 20", para responder: 

Seja o banco de dados de uma empresa varejista, em que há a relação PRODUTO com o seguinte esquema:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**PRODUTO (<ins>CodProduto</ins>, Nome, PrecoUnitario)**<br>
Suponha que há dezenas de preços unitários distintos nos produtos que a empresa vende.

1. Escreva em SQL, use subconsulta(s) independente(s):<br>
_Qual o código e o nome dos produtos que possuem os **N** preços unitários mais caros_?<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**N** é o número de letras do seu primeiro nome.<br>
Por exemplo, se o seu primeiro nome for 'Maria':<br>
&#8718; _Qual o código e o nome dos produtos que possuem os cinco preços unitários mais caros_?

1. Escreva em SQL, use subconsulta(s) correlata(s):<br>
_Qual o código e o nome dos produtos que possuem os **N** preços unitários mais baratos_?<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**N** é o número de letras do seu primeiro nome.<br>
Por exemplo, se o seu primeiro nome for 'Maria', então:<br>
&#8718; _Qual o código e o nome dos produtos que possuem os cinco preços unitários mais baratos_?

CREATE TABLE PRODUTO (CodProduto int, Nome VARCHAR(10), PrecoUnitario FLOAT);
INSERT INTO  PRODUTO VALUES (1, 'PRODUTO 01', 1.11);
INSERT INTO  PRODUTO VALUES (2, 'PRODUTO 02', 2.11);
INSERT INTO  PRODUTO VALUES (3, 'PRODUTO 03', 3.11);
INSERT INTO  PRODUTO VALUES (4, 'PRODUTO 04', 4.11);
INSERT INTO  PRODUTO VALUES (5, 'PRODUTO 05', 5.11);
INSERT INTO  PRODUTO VALUES (6, 'PRODUTO 06', 6.11);
INSERT INTO  PRODUTO VALUES (7, 'PRODUTO 07', 7.11);
INSERT INTO  PRODUTO VALUES (8, 'PRODUTO 08', 8.11);
INSERT INTO  PRODUTO VALUES (9, 'PRODUTO 09', 9.11);
INSERT INTO  PRODUTO VALUES (10, 'PRODUTO 10', 10.11);
INSERT INTO  PRODUTO VALUES (11, 'PRODUTO 11', 11.11);
INSERT INTO  PRODUTO VALUES (12, 'PRODUTO 12', 12.11);
INSERT INTO  PRODUTO VALUES (13, 'PRODUTO 13', 13.11);
INSERT INTO  PRODUTO VALUES (14, 'PRODUTO 14', 14.11);

## Artefatos

1. _Issue_ criada no projeto https://github.com/plinioleitao/bd-2021-1-bxx, cujo título é "Tópico 20", para entender e usar subconsultas em consultas da SQL.
