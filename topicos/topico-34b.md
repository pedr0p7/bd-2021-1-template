## [Tópico T34b] - Projeto Sissa - Dados disponibilizados à disciplina
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

**[Questão 01]:** No escopo da disciplina, há o acesso ao conteúdo completo do _data warehouse_?<br>
**[Resposta]:** Não, a disponibilização de dados é limitada, o acesso ocorre a um subconjunto reduzido dos dados.

**[Questão 02]:** Por que a disponibilização de dados é limitada à disciplina?<br>
**[Resposta]:** Porque o projeto está em curso, várias evidências estão em fase de descoberta e/ou validação e ainda não publicadas, e há conteúdo sensível e passível de mecanismos de segurança e anonimização.

**[Questão 03]:** Apesar do acesso limitado aos dados, há algum esquema publicado para o _data warehouse_, mesmo que em forma de rascunho?<br>
**[Resposta]:** Sim, é um esquema preliminar, favor ver [aqui](https://static.sissa.ufg.br/up_images/modelo.png).

**[Questão 04]:** Como ocorre a interação entre as Instituições de Ensino Superior e os _Serviços Sissa_, com o objetivo de 'alimentar' o _data warehouse_?<br>
**[Resposta]:** Os serviços são fornecidos na forma de APIs, as quais são agrupadas em pacotes, conforme descrito aque [aqui](https://api.sissa.ufg.br/). Este _link_ trata-se da documentação que podemos usar para o entendimento dos dados do subconjunto disponibilizado.

**[Questão 05]:** Como nos é disponibilizado o subconjunto de dados do _data warehouse_?<br>
**[Resposta]:** Três visões nos foram fornecidas, em arquivos formato _csv, _a saber:
- **Visão pré-ingresso**: dados anteriores ao ingresso do discente na Instituição de Ensino Superior.
- **Visão acadêmica**: dados da participação do discente em disciplinas ofertadas pelos cursos de graduação.
- **Visão predição**: dados pertinentes à predição de evasão do cursos de graduação.

**[Questão 06]:** Como 'materizalizamos' os dados das visões  ?<br>
**[Resposta]:** Temos três relações em um banco de dados do **Sistema MariaDB**:
- PREINGRESSO (<ins>id_estudante</ins>, instituicao_ifes, uf_ensino_medio, ano_conclusao_ensino_medio, escola_publica_ensino_medio, nota_corte_curso, preferencia_curso_ingresso, convocacao, ano_ingresso, semestre_ingresso, forma_ingresso, nome_curso, modalidade, area, grau_academico, in_integral, in_matutino, in_vespertino, in_noturno, nota_mec, situacao_curso, turno, situacao_matriz, ano_implantacao, semestre_implantacao, ch_min_obrigatoria, ch_min_naoobrigatoria, ch_min_outra, ch_min_atividade_compl, ch_min_total, status, prazo_conclusao_minimo, prazo_conclusao_medio, prazo_conclusao_maximo)
- **Visão acadêmica**: dados da participação do discente em disciplinas ofertadas pelos cursos de graduação.
- **Visão predição**: dados pertinentes à predição de evasão do cursos de graduação.

## Não há atividade para este tópico, excepcionalmente.
