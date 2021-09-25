## [Tópico T08] - Modelo Entidade Relacionamento (MER) - Primeiros passos
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

**Modelos de dados** promovem a percepção abstrata em níveis para o banco de dados. Nesse sentido, cada modelo de dados se refere a um nível de abstração próprio, para guiar a criação e a evolução de um esquema de banco de dados. A figura a seguir apresenta níveis de abstração para os vários esquemas de um mesmo banco de dados.

<img src="../media/fig-projeto.jpg" width="320">

O **Modelo Entidade Relacionamento (MER)** é comumente aplicado na etapa *projeto conceitual do banco de dados*. O projeto conceitual lida com a *especificação conceitual do banco de dados* (**esquema conceitual**), que é uma representação em uma abstração de alto-nível nível, cujo entendimento é mais próximo de usuários não especializados.

O **projeto conceitual** pelo emprego do **MER** busca abstrair uma **coleção de elementos conceituais** pertinentes aos dados. Essa abstração de elementos conceituais envolve o entendimento das responsabilidades informacionais próprias do banco dados. Cada desses elementos conceituais é inicialmente classificado como **[tipo de] entidade**, **[tipo de] relacionamento entre entidades** ou **atributo**. O processo evolui de forma iterativa e incremental, potencialmente com alterações na classificação inicial, até que amadureça uma representação conceitual do banco de dados, ou seja, um esquema conceitual.

Não é trivial determinar como um elemento conceitual do mundo real será tratado no MER. Dois projetistas distintos podem ter percepções conceituais diferentes sobre o banco de dados de uma aplicação. Então, **precisamos praticar bastante** para aos poucos ganhar maturidade. É um trabalho contínuo, um **bom projetista** sabe que este trabalho nunca terminará.

Algumas questões pertinentes são:
- Como saber **se um dado elemento conceitual é relevante** para o projeto conceitual pelo emprego do MER? Ou seja, esse elemento conceitual deve ser considerado no âmbito do projeto do banco de dados?
- Se o elemento conceitual for relevante, **como classificá-lo** em [tipo de] entidade, [tipo de] relacionamento entre entidades ou atributo? Ou seja, há critério que apoie essa classificação?

O produto do MER – esquema conceitual – pode ser representado por um diagrama, denominado **Diagrama Entidade Relacionamento (DER)**. O DER possui muitas notações, algumas muito conhecidas, tais com as três apresentadas na figura abaixo. O importante é que todas as notações representam as mesmas ideias. Na figura há dois tipos de entidade (DEPARTAMENTO e EMPREGADO) e um tipo de relacionamento (LOTAÇÃO). 

<img src="../media/fig-diagrama-1.jpg" width="410">

Ao ler e reler os três diagramas - Diagramas (a), (b) e (c) na figura - você consegue concluir a seguinte interpretação para o tipo de relacionamento LOTAÇÃO: "*um departamento possui de zero a N empregados lotados, um empregado sempre está lotado em um único departamento*"?
