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

Crie o diretório **topico-30** no seu repositório https://github.com/nomealuno/bd-2021-1-bxx, onde **nomealuno** é o nome da conta do aluno no Github. Este é o repositório que você criou no início da disciplina.

Neste diretório você deverá depositar um arquivo JPG, contendo a imagem de um DER conforme solicitado na atividade. **Atenção às diretrizes abaixo**:
- Use a ferramenta que desejar, desde que a especificação do DER tenha **precisamente** a notação apresentada no [Tópico 22](./topico-22.md):
  - Sugestão: use a ferramenta [Dia](http://dia-installer.de/), que é uma ferramenta de desenho:
    - para especificar o DER, selecione a *Folha* **ER** (em vez da *Folha* **Banco de Dados**);
    - ao final, exporte o desenho para um arquivo JPG.
- Ao 'depositar' o arquivo no diretório, checar se as dimensões da imagem do diagrama estão ajustadas à area de apresentação no GitHub (não deve ser muito pequeno a ponto de tornar-se ilegível, nem grande demais a ponto de ser necessário **rolar** (*to scroll*) para visualizar).
- Faça você mesmo, evite olhar respostas prontas.<br> Novamente, convém citar Cora Coralina para esclarecer o objetivo da atividade: "O que vale na vida não é o ponto de partida e sim a caminhada. Caminhando e semeando, no fim terás o que colher".

A atividade considera o DER de uma universidade, conformne ilustrado na figura a seguir.

<img src="../media/fig-der-universidade.jpg" width="600">

1. Quais as alterações no DER tal que as consultas em **Reflexões 06** sejam atendidas?<br>
Favor ver as consultas em **Reflexões 06** no [Tópico 25c](../topicos/topico-25c.md).<br>
Observações importantes:<br>
&#9786; O ponto de partida é o DER resultante das consultas em **Reflexões 05** no [Tópico 25c](../topicos/topico-25c.md).<br>
&#9786; Não remova qualquer elemento do DER em **Reflexões 05**, apenas acrescente novos elementos.<br>
&#9786; Faça marcações coloridas (bolas verdes) em todos os elementos que você acrescentou.<br>
&#9786; Somente os elementos que você acrescentou devem ter as marcações coloridas.<br>
&#9786; É necessário 'desenhar' o DER completo (não apenas as partes acrescentadas).

## Artefatos

1. Diretório **topico-28**, criado no repositório do estudante, contendo um arquivo com a imagem JPG do DER solicitado.

