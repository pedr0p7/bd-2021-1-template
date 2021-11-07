## [Tópico T34b] - Projeto Sissa - Dados disponibilizados à disciplina
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

**[Questão 01]:** No escopo da disciplina, há o acesso ao conteúdo completo do _data warehouse_?<br>
**[Resposta]:** Não, a disponibilização de dados é limitada, o acesso ocorre a um subconjunto reduzido dos dados.

**[Questão 02]:** Por que a disponibilização de dados é limitada à disciplina?<br>
**[Resposta]:** Porque o projeto está em curso, várias evidências estão em fase de descoberta e/ou validação e ainda não publicadas, e há conteúdo sensível e passível de mecanismos de segurança e [anonimização](https://anonimizacao.com.br/).

**[Questão 03]:** Apesar do acesso limitado aos dados, há algum esquema publicado para o _data warehouse_, mesmo que em forma de rascunho?<br>
**[Resposta]:** Sim, é um esquema preliminar, favor ver [aqui](https://static.sissa.ufg.br/up_images/modelo.png).

**[Questão 04]:** Como ocorre a interação entre as Instituições de Ensino Superior e os _Serviços Sissa_, com o objetivo de 'alimentar' o _data warehouse_?<br>
**[Resposta]:** Os serviços são fornecidos na forma de APIs, as quais são agrupadas em pacotes, conforme descrito [aqui](https://api.sissa.ufg.br/). Este _link_ trata-se da documentação disponível, que podemos usar para o entendimento dos dados do subconjunto disponibilizado. Mas requer _minerar_ os conceitos abordados.

**[Questão 05]:** Como nos é disponibilizado o subconjunto de dados do _data warehouse_?<br>
**[Resposta]:** Três visões nos foram fornecidas, em arquivos formato _csv_, a saber:
- **Visão pré-ingresso**: dados anteriores ao ingresso do discente na Instituição de Ensino Superior.
- **Visão acadêmica**: dados da participação do discente em disciplinas ofertadas pelos cursos de graduação.
- **Visão predição**: dados pertinentes à predição de evasão do cursos de graduação.

**[Questão 06]:** Como foram 'materizalizados' os dados das visões disponobilizadas ?<br>
**[Resposta]:** Três relações foram criadas em um banco de dados - denominado **sissa** - no **Sistema MariaDB**:
- **PREINGRESSO** (<ins>id_estudante</ins>, instituicao_ifes, uf_ensino_medio, ano_conclusao_ensino_medio, escola_publica_ensino_medio, nota_corte_curso, preferencia_curso_ingresso, convocacao, ano_ingresso, semestre_ingresso, forma_ingresso, nome_curso, modalidade, area, grau_academico, in_integral, in_matutino, in_vespertino, in_noturno, nota_mec, situacao_curso, turno, situacao_matriz, ano_implantacao, semestre_implantacao, ch_min_obrigatoria, ch_min_naoobrigatoria, ch_min_outra, ch_min_atividade_compl, ch_min_total, status, prazo_conclusao_minimo, prazo_conclusao_medio, prazo_conclusao_maximo)
- **TURMAS** (id_estudante, nome_disciplina, ch_pratica, ch_teorica, ch_total, credito_total_disciplina, credito_pratica_disciplina, credito_teorica_disciplina, periodo_sugerido_disciplina, natureza, nucleo, ano_oferta_disciplina, semestre_oferta_disciplina, qtd_vagas_total, qtd_vagas_externas, ano_matricula, semestre_matricula, data_matricula, nota, frequencia, status_disciplina)
- **PREDICAO** (id_estudante, Classe, Risco, Probabilidade_da_Classe, Semestres_Saida, Proba_Sem, Metodo_de_ML)

**[Questão 07]:** Como ter acesso aos dados materializados ?<br>
[Resposta]: Use este [link](http://200.137.197.36/phpMyAdmin/) e selecione:
- Usuário: _discente_
- Senha: _password_
- Escolha de servidor: _MariaDB-server_

Favor acessar o ambiente e explorar o banco de dados.

**[Outras Questões]:**

- Qual a quantidade de _tuplas_ em cada relação? (Obs. A relação TURMAS não foi completamente 'carregada' no _data warehouse_, devido a limitações da máquina virtual.
- Qual o domínio de cada atributo?
- Que atributos podem identificar o discente?
- Que atributos podem identificar a instituição de ensibo?

## Não há atividade para este tópico, excepcionalmente.
