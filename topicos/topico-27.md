## [Tópico T27] - Tempo para convergir ...
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

```diff
+ Vários foram os conceitos estudados até o momento, conforme a nossa ementa.
- Tenhamos, em tal caso, uma oportunidade para 'exercícios de revisão'.
@@ Enfim, um breve momento para convergir nossas percepções. @@
```

### Exercício 01

Foi solicitada a implementação de uma nova cláusula (função) para a SQL, denominada **UNIQUE**, que é avaliada como **True** quando a subconsulta não retornar _tuplas_ repetidas. Como esta cláusula ainda não foi implementada pelo SGBD, você poderia escrever uma **Consulta SQL Alternativa** para o exemplo abaixo?<br>(para melhor entendimento, veja a _Consulta SQL Alternativa_ do exemplo com a cláusula EXISTS): 

|Consulta SQL Original|Consulta SQL Alternativa|Significado|
|-|-|-|
|SELECT Pnome, Unome<br>FROM FUNCIONARIO AS F<br>WHERE **EXISTS** (<br>&nbsp;&nbsp;SELECT Nome_dependente<br>&nbsp;&nbsp;FROM DEPENDENTE AS D<br>&nbsp;&nbsp;WHERE F.Cpf = D.Fcpf )|SELECT Pnome, Unome<br>FROM FUNCIONARIO AS F<br>WHERE 0 < (<br>&nbsp;&nbsp;SELECT COUNT(\*)<br>&nbsp;&nbsp;FROM DEPENDENTE AS D<br>&nbsp;&nbsp;WHERE F.Cpf = D.Fcpf )|Qual o primeiro e último nomes dos funcionários<br>que possuem algum dependente?|
|SELECT Pnome, Unome<br>FROM FUNCIONARIO AS F<br>WHERE **UNIQUE** (<br>&nbsp;&nbsp;SELECT Nome_dependente<br>&nbsp;&nbsp;FROM DEPENDENTE AS D<br>&nbsp;&nbsp;WHERE F.Cpf = D.Fcpf )|???????????????|Qual o primeiro e último nomes dos funcionários<br>cujos dependentes não têm nomes repetidos?|

### Exercício 02

Considere o esquema de banco de dados sobre uma biblioteca descrito a seguir. Os atributos em negrito referem-se à chave primária de cada relação. 

A relação ENDERECO (**Identificador**, Logradouro, CEP, Cidade, UF) representa os endereços de pessoas e editoras. 

A relação PESSOA (**CPF**, Nome, Sexo, DataNascimento, Identificador) refere-se às pessoas que solicitam empréstimos de livros: o atributo Identificador é uma chave estrangeira que referencia ENDERECO; duas ou mais pessoas podem compartilhar um mesmo endereço; o endereço de uma pessoa não é obrigatório no banco de dados. 

A relação EDITORA (**Codigo**, Nome, Identificador) relaciona-se às editoras de livros: o atributo Identificador é uma chave estrangeira que referencia ENDERECO; duas ou mais editoras não podem compartilhar um mesmo endereço; o endereço de qualquer editora é obrigatório no banco de dados. 

A relação LIVRO (**ISBN**, Titulo, AnoDeEdicao, Codigo) refere-se aos livros que podem ser emprestados: o atributo Codigo é uma chave estrangeira que referencia à relação EDITORA; todos os atributos devem ter algum valor em cada tupla da relação; dois ou mais livros podem compartilhar uma mesma editora. 

A relação AUTOR (**Numero**, Nome) denota os autores de livros. 

A relação AUTORIA (**ISBN, Numero**) associa autores a livros: ISBN e Numero são chaves estrangeiras que referenciam LIVRO e AUTOR, respectivamente; um livro pode ter vários autores, e um autor pode estar associado a vários livros. 

A relação EMPRESTIMO (**CPF, ISBN, DataInicio**, DataFinalPrevista, DataFinalReal) é pertinente aos empréstimos de livros: CPF é uma chave estrangeira que referencia PESSOA; ISBN é uma chave estrangeira que referencia LIVRO; os atributos DataInicio e DataFinalPrevista referem-se à data de retirada do livro e à data prevista de devolução, respectivamente, ambos com valores obrigatórios no banco de dados; o atributo DataFinalReal denota a data efetiva de devolução do livro, e somente possuirá algum valor quando o livro em questão tiver sido devolvido pela pessoa; uma pessoa pode tomar emprestado vários livros e um livro pode ser emprestado várias vezes. 

## Atividade (data limite: **xx/xx/xxxx 23h59min59s**)

Com respeito ao **Exercício 02**, criar uma _issue_ no projeto https://github.com/plinioleitao/bd-2021-1-bxx, com o título "Tópico 27", para responder: 

1. De acordo com as restrições de integridade no banco de dados,<br>
(a) uma editora pode ter mais de um endereço.<br>
(b) uma pessoa pode ter mais de um endereço.<br>
(c) um livro pode ser emprestado várias vezes para uma mesma pessoa.<br> 
(d) um livro pode ser editado por várias editoras e pode ter vários autores distintos.<br>
(e) Nenhum das alternativas anteriores.<br>
RESPOSTA (c)

2. Valores nulos são permitidos para alguns atributos do banco de dados. Um atributo que pode ter valor nulo é:<br>
(a) Codigo em LIVRO.<br>
(b) Identificador em PESSOA.<br>
(c) Identificador em EDITORA.<br>
(d) DataFinalPrevista em EMPRESTIMO.<br>
(e) Nenhum das alternativas anteriores.<br>
RESPOSTA (b)

3. Valores de alguns atributos devem ser únicos entre as tuplas de uma relação, tal como o atributo<br>
(a) Numero em AUTOR.<br>
(b) ISBN em AUTORIA.<br>
(c) ISBN em EMPRESTIMO.<br>
(d) Numero em AUTORIA.<br>
(e) Nenhum das alternativas anteriores.<br>
RESPOSTA (a)

4. Uma informação obtida a partir do banco de dados é:<br>
(a) a idade de cada autor.<br>
(b) os livros comprados no último mês.<br>
(c) a quantidade de dias de atraso dos empréstimos devolvidos com atraso.<br>
(d) o nome das editoras que mudaram de endereço mais de uma vez no último ano.<br>
(e) Nenhum das alternativas anteriores.<br>
RESPOSTA (c)

## Artefatos

1. _Issue_ criada no projeto https://github.com/plinioleitao/2021-1-bxx, cujo título é "Tópico 27", para rever conceitos aplicados do modelo relacional.
