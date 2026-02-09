# Projeto EngDados

## Objetivo Principal

O projeto Final de Engenharia de Dados será aberto e envolverá **operacionalizar** uma solução de dados em um **ambiente de produção**.

## Principais Tarefas

A primeira tarefa principal será buscar um **problema**. Uma abordagem válida seria utilizar um **Dataset público** disponível em plataformas como o [Kaggle](https://www.kaggle.com/datasets), [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php) ou [Google Dataset Search](https://datasetsearch.research.google.com/). Escolha um conjunto de dados que seja relevante para um problema de negócio ou interesse pessoal, e que permita a aplicação de técnicas de Engenharia de Dados.

!!! note "Importante"
    Você também pode optar por construir o seu próprio conjunto de dados, coletando dados de APIs públicas, web scraping ou outras fontes.

    Certifique-se de que os dados coletados sejam suficientes para o escopo do projeto.

Depois de localizar um conjuntos de dados, a próxima etapa será elencar as necessidades de uma área cliente. Por exemplo, você pode supor que existe a necessidade de que os dados estejam disponíveis para serem consumidos por um *Dashboard*, ou que cientistas de dados precisam dos dados para treinar um modelo. Você precisará ser criativo para definir essas necessidades!

Em seguida, defina as **tarefas de Engenharia de Dados** necessárias para satisfazer essas necessidades. Isso pode incluir:

- Ingestão de dados
- Limpeza e transformação de dados
- Armazenamento e disponibilização de dados
- Criação de pipelines de dados
- Garantia de qualidade dos dados
- Documentação
- Observabilidade
- etc.

## Grupos

O projeto pode ser desenvolvido individualmente ou em duplas.

### Aceitar a Tarefa

Todas as entregas serão feitas via github classroom.

[Crie seu grupo](https://classroom.github.com/a/NLEJWKPH) para iniciar a tarefa.

!!! danger "Atenção"
    O primeiro membro cria o grupo, enquanto o segundo apenas se junta ao grupo.

## Critérios de Avaliação

- **I**:
       - Não entregou ou o projeto ficou muito abaixo das expectativas.

- **D**:
    - Entregou o projeto, mas contém erros (códigos ou scripts com falhas) OU
    - Contribuição altamente desproporcional entre os membros da equipe.

- **C**:
    - Entregou um vídeo explicando os detalhes do projeto (problema, dados, principais detalhes de engenharia de dados) E
    - O projeto roda sem erros E
    - O repositório do projeto e outros recursos estão bem organizados E
    - O projeto é reproduzível, ou seja, há uma boa documentação do projeto, código-fonte, dados e *pipelines* E
    - Utiliza logging estruturado para eventos importantes do pipeline E
    - Há um processo claro para coletar (se aplicável), armazenar e pré-processar dados (camadas da arquitetura *Medalion*).
    - Implementa um modelo de dados dimensional (Star Schema ou Snowflake Schema) ou One Big Table (OBT) para análise.

!!! warning "Importante"
    Caso algum dos critérios das rubricas **B** ou **A** não se apliquem ao seu projeto, **converse com o professor** para ajustar os critérios de avaliação.

    Deixe claro no README do projeto quais critérios não se aplicam e o porquê.

- **B (fez a maioria)**:
    - Utilizou um framework adequado de orquestração (por exemplo, **Prefect** ou **Airflow**) para gerenciar o pipeline de dados, com tratamento de falhas (*retries*) e dependências claras.
    - Implementa monitoramento de métricas (ex: Prometheus) para acompanhar a saúde e performance do pipeline ou da aplicação.
    - Utiliza um sistema de filas de mensagens (ex: RabbitMQ) para desacoplar componentes e lidar com picos de carga na ingestão de dados.
    - Otimiza consultas SQL utilizando índices apropriados (B-Tree, BRIN, GIN) e/ou views materializadas para melhorar a performance.


- **A (fez a maioria)**:
    - Implementa *tracing* distribuído (ex: **Jaeger** com **OpenTelemetry**) para depurar e analisar a latência em sistemas com múltiplos serviços.
    - Utiliza IaC (Infraestrutura como Código) para criar e gerenciar a infraestrutura em ambiente de nuvem (ex: AWS EC2, S3, Glue, EMR).
    - O projeto utiliza um Data Lakehouse (ex: Databricks com Delta Lake/Iceberg) para unificar o armazenamento e processamento de dados estruturados e não estruturados.
    - Implementa *read replicas* para distribuir a carga de leitura e melhorar a disponibilidade do banco de dados.
    - Demonstra compreensão avançada de otimização de consultas, incluindo paginação baseada em cursor para APIs e análise detalhada de planos de execução.

## Prazos

- **02 de Novembro**: Criar grupo e repositório.
- **09 de novembro**: Entrega parcial. Problema definido (preencher README) com dados disponíveis. Commit no github.com com evidências de que a tarefa foi realizada (não faça commit de arquivos grandes).
- **30 de novembro**: Entrega final. Nesta entrega, será necessário adicionar um relatório e um vídeo curto descrevendo o projeto implementado e suas funcionalidades.