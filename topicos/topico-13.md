## [Tópico T13] - Álgebra Relacional - Junção Externa
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

Para apoiar os exemplos das operações da Álgebra Relacional, considere a ilustração abaixo do **BD Empresa**.

<img src="../media/fig-mr-2.jpg" width="450">

### Operação JUNÇÃO EXTERNA (OUTER JOIN)

As variações da Operação JUNÇÃO **estudadas até o momento** (a saber, JUNÇÃO THETA, EQUIJUNÇÃO e JUNÇÃO NATURAL) são denominadas JUNÇÃO INTERNA (INNER JOIN):
- Na JUNÇÃO INTERNA entre **R** e **S**, as combinações de _tuplas_ de **R** e **S** (ou seja, a concatenação de uma _tupla_ de **R** com uma _tupla_ de **S**) devem atender ao **predicado de junção**:
  - as combinações, nas quais o **predicado de junção** é avaliado como falso, são eliminadas do (não estão presentes no) resultado da junção.

Por exemplo, "_Qual o nome dos empregados e o nome dos departamentos que gerenciam?"_:
- uma expressão para a consulta é:
  - **π <sub>Pnome, Unome, Dnome</sub> (FUNCIONARIO ⨝ <sub>Cpf = Cpf_gerente</sub> DEPARTAMENTO)**;
- o predicado de junção presente nesta expressão é:
  - **Cpf = Cpf_gerente**;
- o resultado da junção **somente inclui** as _tuplas_ em que o _predicado de junção_ é avaliado como _verdadeiro_:
  - o resultado da junção está a seguir, conforme a ilustração do **BD Empresa** mostrada acima.

|Pnome|Unome|Dnome|
|-|-|-|
|Fernando|Wong|Pesquisa|
|Jennifer|Souza|Administração|
|Jorge|Brito|Matriz|

#### JUNÇÃO EXTERNA Exemplo 1:

No exemplo "_Qual o nome dos empregados e, para aqueles que são gerentes, o nome dos departamentos que gerenciam?"_:
- A consulta é uma JUNÇÃO EXTERNA À ESQUERDA;
- A expressão é:
  - **π <sub>Pnome, Unome, Dnome</sub> (FUNCIONARIO ⟕ <sub>Cpf = Cpf_gerente</sub> DEPARTAMENTO)** ;
  - observe o uso do símbolo ⟕ (em vez de ⨝).
- O resultado da consulta é exibido abaixo.

|Pnome|Unome|Dnome|
|-|-|-|
|João|Silva|NULL|
|Fernando|Wong|Pesquisa|
|Alice|Zelaya|NULL|
|Jennifer|Souza|Administração|
|Ronaldo|Lima|NULL|
|Joice|Leite|NULL|
|André|Pereira|NULL|
|Jorge|Brito|Matriz|

#### JUNÇÃO EXTERNA Exemplo 2:

No exemplo "_Qual o nome dos empregados e, para aqueles que possuem dependentes, o nome dos seus dependentes?"_:
- A consulta é uma JUNÇÃO EXTERNA À ESQUERDA;
- A expressão é:
  - **π <sub>Pnome, Unome, Nome_dependente</sub> (FUNCIONARIO ⟕ <sub>Cpf = Fcpf</sub> DEPENDENTE)** ;
  - observe o uso do símbolo ⟕ (em vez de ⨝).
- O resultado da consulta é exibido abaixo.

|Pnome|Unome|Nome_dependente|
|-|-|-|
|João|Silva|Michael|
|João|Silva|Alicia|
|João|Silva|Elizabeth|
|Fernando|Wong|Alicia|
|Fernando|Wong|Tiago|
|Fernando|Wong|Janaina|
|Alice|Zelaya|NULL|
|Jennifer|Souza|Antonio|
|Ronaldo|Lima|NULL|
|Joice|Leite|NULL|
|André|Pereira|NULL|
|Jorge|Brito|NULL|

#### JUNÇÃO EXTERNA Exemplo 3:

Na JUNÇÃO EXTERNA entre R e S, a relação resultante possui:
- as _tuplas_ do resultado da JUNÇÃO INTERNA; e
- as _tuplas_ de **R e/ou S**, quando o **predicado de junção** não é avaliado como verdadeiro.

Há três variações de JUNÇÃO EXTERNA:
- JUNÇÃO EXTERNA À ESQUERDA (LEFT OUTER JOIN), cujo símbolo é ⟕ ;
- JUNÇÃO EXTERNA À DIREITA (RIGHT OUTER JOIN), cujo símbolo é ⟖ ;
- JUNÇÃO EXTERNA COMPLETA (FULL OUTER JOIN), cujo símbolo é ⟗ .

Abaixo são mostrados exemplos para as três variações da operação JUNÇÃO EXTERNA.

<img src="../media/fig-algebra-juncao-externa.jpg" width="500">

## Atividade (data limite: **xx/xx/xxxx 23h59min59s**)

Seja o esquema relacional simplificado abaixo:
-	VENDE ( Bar, Cerveja )
-	GOSTA ( Pessoa, Cerveja )

A relação VENDE refere-se aos bares e às marcas de cerveja que lá são vendidas.<br>
A relação GOSTA representa marcas de cervejas e pessoas que gostam delas.

Criar uma _issue_ no projeto https://github.com/plinioleitao/bd-2021-1-bxx, com o título "Tópico 13", para responder:  

Escreva em álgebra relacional as seguintes consultas:
1. Quais as cervejas vendidas no bar “Pipoca”?
1. Quais as pessoas que gostam de alguma(s) cerveja(s) vendida(s) no bar “Pipoca”?
1. Quais as pessoas que não gostam de qualquer das cervejas vendidas no bar “Pipoca”?

IMPORTANTE: Use a sintaxe da Álgebra Relacional conforme os exemplos apresentados até então.

RESPOSTAS:
1. RESULT ← π Cerveja ( σ Bar=”Pipoca” (VENDE) )
1. RESULT ← π Pessoa ( σ Bar=”Pipoca” (VENDE * GOSTA) )
3. TEMP ← π Pessoa ( σ Bar=”Pipoca” (VENDE * GOSTA) )<br>
RESULT ← π Pessoa (GOSTA) - TEMP

## Artefatos

1. _Issue_ criada no projeto https://github.com/plinioleitao/bd-2021-1-bxx, cujo título é "Tópico 13", para praticar operações da *álgebra relacional*.
