## [Tópico T34a] - Projeto SISSA
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### Contexto

**Sissa** denota uma plataforma baseada em Inteligência Artificial que combina integração de dados acadêmicos, monitoramento eficiente de indicadores, previsão de sucesso do estudante, capacitação de tutores e interações por pares em um sistema que apoia o estudante.

Mais informações, favor clicar [aqui](https://sissa.ufg.br/).

### Integração de dados

Integração de dados se refere ao acesso, preferencialmente uniforme, a fontes de dados autônomas e heterogêneas. Noutras palavras, ter visão unificada dos dados de múltiplas fontes de dados díspares, internas e/ou externas. 

Algumas observações pertinenetes:
- O acesso aos dados (por exemplo, consultas) deve ocorrer de maneira uniforme (conteúdo e estrutura), mesmo no cenário de fontes heterogêneas:
  - também, deve haver independência em relação a alterações nas fontes de dados;
  - por exemplo, as fontes podem alterar seus formatos de dados e padrões de acesso a qualquer momento.
- Envolve fontes de dados que foram desenvolvidas independentemente umas das outras:
  - dados em bases relacionais, arquivos com conteúdo não estruturado, arquivos binários, arquivos JSON, arquivos XML, etc.
  - dados disponíveis por sistemas de gerencamento, por conexão/serviço Web, por acesso simples a um diretório, etc.
- O acesso aos dados podem requerer privacidade:
  - acesso restrito a usuários e a operações sobre os dados;
  - acesso apropriado no caso de dados sensíveis.
- O aumento do número de fontes representa um acréscimo importante aos desafios enfrentados.

### Estratégias de integração de dados:<br>Consolidação de dados _versus_ Virtualização de dados

1. **Consolidação de dados**<br>
Envolve a combinação de dados de fontes distintas, removendo suas redundâncias, eliminando quaisquer erros e agregando-os em um único armazenamento de dados, tal como um _data warehouse_.<br>Em geral, emprega uma abordagem do tipo ETL (_Extract_, _Transform_, _Load_):
  - Extração: Antes que os dados possam ser movidos para um novo destino, eles devem primeiro ser extraídos de sua origem. Nesta primeira etapa do processo ETL, dados estruturados e não estruturados são importados e consolidados em um único repositório. Os dados brutos podem ser extraídos de uma ampla variedade de fontes, incluindo:

Bancos de dados existentes e sistemas legados
Ambientes em nuvem, híbridos e locais
Aplicativos de vendas e marketing
Dispositivos móveis e aplicativos
Sistemas de CRM
Plataformas de armazenamento de dados
Armazéns de dados
Ferramentas analíticas

Como a consolidação de dados é o processo clássico de integração de dados que aproveita a tecnologia ETL, os dois termos às vezes são usados alternadamente. Envolve a combinação de dados de fontes distintas, removendo suas redundâncias, eliminando quaisquer erros e agregando-os em um único armazenamento de dados como um data warehouse. Embora complexo, ele se encaixa na maioria dos casos. O estilo de entrega para consolidar dados é o armazenamento de dados comum que abordamos a seguir.

A virtualização de dados apresenta uma abordagem moderna para integração de dados. Ao contrário das soluções ETL, que replicam dados, a virtualização de dados deixa os dados nos sistemas de origem, simplesmente expondo uma visão integrada de todos os dados aos consumidores de dados.

ETL / ELT
ETL, ou extrair, transformar, carregar, é o processo de replicar dados de fontes de dados e carregar esses dados em bancos de dados e data warehouses para armazenamento. Ferramentas ETL modernas também fornecem ELT, transpondo as etapas de carregamento e transformação de dados e aproveitando o banco de dados subjacente para transformar os dados depois de carregados.

Essa estratégia é popular para lidar com grandes volumes de dados e é a abordagem tradicional para integração de dados. É ideal para executar uma ampla gama de iniciativas corporativas, desde BI e análises a IA, desenvolvimento de aplicativos e muito mais em cima de um banco de dados central ou data warehouse. Por definição, essa abordagem usa integração de dados pura - integrando seus dados sem integrar seus aplicativos.

Se você precisa gerenciar e automatizar suas integrações de dados em escala, confira CData Sync, nossa solução ETL / ELT líder para integração de dados. Com o Sync, você pode replicar dados de mais de 100 aplicativos e fontes de dados em mais de 30 bancos de dados e depósitos para automatizar a replicação de dados.


## Não há atividade para este tópico, excepcionalmente.
