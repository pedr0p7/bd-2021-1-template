## [Tópico T30] - Mapeamento MER para MR (parte 3)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

O conteúdo apresentado usa o esquema conceitual do **BD Empresa**, conforme abaixo.

<img src="../media/fig-der-empresa.jpg" width="400">

### Regra 06 - Mapeamento de Atributo Multivalorado

Para cada atributo multivalorado **_M_**, pertencente ao tipo de entidade **E**:
- O tipo de entidade **E** é mapeado pela relação **T**:
  - a chave primária de **T** é **_Key_**;
  - a atributo **_M_** não deve ser incluído em **T**.
- Para mapear o atributo multivalorado multivalorado **_M_** em **E**:
  - criar uma nova relação **T\_M**;
  - incluir em **T\_M**:
    - um atributo correspondente ao próprio atributo multivalorado **_M_**;
    - um atributo correspondente à chave estrangeira, denominado **_Key_**, a qual referencia a chave primária da relação **T**;
  - a chave primária de **T\_M** é composta por:
    - o atributo **_Key_**; e
    - o atributo **_M_**.

<img src="../media/fig-mapeamento-atributo-multivalorado.jpg" width="200">

Sobre o BD Empresa, a aplicação desta regra resulta em (_realce em **negrito**_):

|Esquema de relação|
|-|
|FUNCIONARIO (Pnome, Minicial, Unome, Cpf, Datanasc, Endereco, Sexo, Salario, Cpf_supervisor, Dnr)<br>FUNCIONARIO (Cpf) IS PRIMARY KEY<br>FUNCIONARIO (Cpf_supervisor) REFERENCES FUNCIONARIO (Cpf)<br>FUNCIONARIO (Dnr) REFERENCES DEPARTAMENTO (Dnumero)|
|DEPARTAMENTO (Dnome, Dnumero, Cpf_gerente, Data_inicio_gerente)<br>DEPARTAMENTO (Dnumero) IS PRIMARY KEY<br>DEPARTAMENTO (Cpf_gerente) REFERENCES FUNCIONARIO (Cpf)|
|PROJETO (Projnome, Projnumero, Projlocal, Dnum)<br>PROJETO (Projnumero) IS PRIMARY KEY<br>PROJETO (Dnum) REFERENCES DEPARTAMENTO (Dnumero)|
|DEPENDENTE (Fcpf, Nome_dependente, Sexo, Datanasc, Parentesco)<br>DEPENDENTE (Fcpf, Nome_dependente) IS PRIMARY KEY<br>DEPENDENTE (Fcpf) REFERENCES FUNCIONARIO (Cpf)|
|TRABALHA_EM (Fcpf, Pnr, Horas)<br>TRABALHA_EM (Fcpf, Pnr) IS PRIMARY KEY<br>TRABALHA_EM (Fcpf) REFERENCES FUNCIONARIO (Cpf)<br>TRABALHA_EM (Pnr) REFERENCES PROJETO (Projnumero)|
|**LOCALIZACAO_DEP (Dnumero, Dlocal)<br>LOCALIZACAO_DEP (Dnumero, Dlocal) IS PRIMARY KEY<br>LOCALIZACAO_DEP (Dnumero) REFERENCES DEPARTAMENTO (Dnumero)**|

### Regra 07 - Mapeamento de Tipo de Relacionamento N-ário

Seja o tipo de relacionamento n-ário R (**n > 2**) no esquema conceitual (esquema ER), conforme a figura abaixo:
- **E<sub>1</sub>**, **E<sub>2</sub>** e **E<sub>3</sub>** são os tipos de entidade que participam de **R**.
- **T<sub>1</sub>**, **T<sub>2</sub>** e **T<sub>3</sub>** correspondem às relações mapeadas a partir de **E<sub>1</sub>**, **E<sub>2</sub>** e **E<sub>3</sub>**, respectivamente.

<img src="../media/fig-mapeamento-relacionamento-5.jpg" width="350">

Para cada tipo de relacionamento n-ário **R**, tal que **n > 2**, criar uma nova relação **S** para representar R:
- Incluir em **S** as chaves estrangeiras que referenciam as chaves primárias das relações que representam os tipos de entidades participantes:
  - incluir **Key<sub>1</sub>** que referencia **T<sub>1</sub>**;
  - incluir **Key<sub>2</sub>** que referencia **T<sub>2</sub>**;
  - incluir **Key<sub>3</sub>** que referencia **T<sub>3</sub>**.
- A chave primária de **S** é, em geral, uma combinação de todas as chaves estrangeiras que fazem referência às relações que representam os tipos de entidade participantes:
  - **S<sub>1</sub> (Key<sub>1</sub>, Key<sub>2</sub>, Key<sub>3</sub>) IS PRIMARY KEY**
    - entretanto, se as restrições de cardinalidade em qualquer um dos tipos de entidade **E<sub>i</sub>** (que participam de **R**) for 1, a chave primária de **S** não precisa incluir o atributo de chave estrangeira que faz referência à relação **T<sub>i</sub>**.
- Incluir na relação **S** todos os atributos simples (ou componentes simples de atributos compostos) do tipo de relacionamento **R**.

A aplicação desta regra ao esquema da figura acima resulta em (_realce em **negrito**_):

|Esquema de relação|
|-|
|**T<sub>1</sub> (Key<sub>1</sub>, A<sub>1</sub>, A<sub>2</sub>)<br>T<sub>1</sub> (Key<sub>1</sub>) IS PRIMARY KEY**|
|**T<sub>2</sub> (Key<sub>2</sub>, B<sub>1</sub>, B<sub>2</sub>)<br>T<sub>2</sub> (Key<sub>2</sub>) IS PRIMARY KEY**|
|**T<sub>3</sub> (Key<sub>3</sub>, C<sub>1</sub>, C<sub>2</sub>)<br>T<sub>3</sub> (Key<sub>3</sub>) IS PRIMARY KEY**|
|**S (Key<sub>1</sub>, Key<sub>2</sub>, Key<sub>3</sub>, X)<br>S (Key<sub>1</sub>, Key<sub>2</sub>, Key<sub>3</sub>) IS PRIMARY KEY<br>S (Key<sub>1</sub>) REFERENCES T<sub>1</sub> (Key<sub>1</sub>)<br>S (Key<sub>2</sub>) REFERENCES T<sub>2</sub> (Key<sub>2</sub>)<br>S (Key<sub>3</sub>) REFERENCES T<sub>3</sub> (Key<sub>3</sub>)**|

> Como determinar a restrição de cardinalidade (e a restrição de participação) em tipos de relacionamento n-ário, tal que **n > 2**?

<img src="../media/fig-mapeamento-relacionamento-6.jpg" width="450">

## Atividade (data limite: **xx/xx/xxxx 23h59min59s**)

Criar uma _issue_ no projeto https://github.com/plinioleitao/bd-2021-1-bxx, com o título "Tópico 30", para responder: 

A atividade considera o DER do BD Universidade, conforme ilustrado na figura a seguir.

<img src="../media/fig-der-universidade.jpg" width="600">

1. Apresente um esquema lógico, segundo o Modelo Entidade Relacionamento, pertinente ao DER do BD Universidade.<br>
Observações importantes:<br>
&#9786; Siga rigorosamente a seguinte notação:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TAB1 (A1, A2, A3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TAB1 (A1) IS PRIMARY KEY<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TAB2 (B1, B2, CE)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TAB2 (B1, B2) IS PRIMARY KEY<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TAB2 (CE) REFERENCES TAB1 (A1)<br>
&#9786; Não apresente a aplicação de cada regra.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Mostre apenas o esquema lógico final após aplicar todas as regras.<br>
&#9786; Um aluno pode ter várias notas iguais em uma mesma turma.

RESPOSTA<br>
ALUNO (MatriculaAluno, Nome, DataIngresso)<br>
ALUNO (MatriculaAluno) IS PRIMARY KEY<br>
CURSO (NumeroCurso, Nome, Diretor, Creditos)<br>
CURSO (NumeroCurso) IS PRIMARY KEY<br>
DISCIPLINA (CodigoDisciplina, Ementa, Descricao)<br>
DISCIPLINA (CodigoDisciplina) IS PRIMARY KEY<br>
PROFESSOR (MatriculaProfessor, Nome, NumeroCurso)<br>
PROFESSOR (MatriculaProfessor) IS PRIMARY KEY<br>
PROFESSOR (NumeroCurso) REFERENCES CURSO (NumeroCurso)<br>
TURMA (CodigoDisciplina, CodigoTurma, Semestre, Sala, Horario, MatriculaProfessor)<br>
TURMA (CodigoDisciplina, CodigoTurma, Semestre) IS PRIMARY KEY<br>
TURMA (CodigoDisciplina) REFERENCES DISCIPLINA (CodigoDisciplina)<br>
TURMA (MatriculaProfessor) REFERENCES PROFESSOR (MatriculaProfessor)<br>
TURMA_ALUNO (MatriculaAluno, CodigoDisciplina, CodigoTurma, Semestre)<br>
TURMA_ALUNO (MatriculaAluno, CodigoDisciplina, CodigoTurma, Semestre) IS PRIMARY KEY<br>
TURMA_ALUNO (MatriculaAluno) REFERENCES ALUNO (MatriculaAluno)<br>
TURMA_ALUNO (CodigoDisciplina, CodigoTurma, Semestre) REFERENCES TURMA (CodigoDisciplina, CodigoTurma, Semestre)<br>
TURMA_ALUNO_NOTA (MatriculaAluno, CodigoDisciplina, CodigoTurma, Semestre, Sequencia, Nota)<br>
TURMA_ALUNO_NOTA (MatriculaAluno, CodigoDisciplina, CodigoTurma, Semestre, Sequencia) IS PRIMARY KEY<br>
TURMA_ALUNO_NOTA (MatriculaAluno, CodigoDisciplina, CodigoTurma, Semestre) REFERENCES TURMA_ALUNO (MatriculaAluno, CodigoDisciplina, CodigoTurma, Semestre)

## Artefatos

1. _Issue_ criada no projeto https://github.com/plinioleitao/bd-2021-1-bxx, cujo título é "Tópico 30", para exercitar o mapeamento entre esquemas segundo o Modelo Entidade Relacionamento e segundo o Modelo relacional.
