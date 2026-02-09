# Introdução

Durante o curso, exploramos diversos aspectos práticos da engenharia de dados, desde a construção de *pipelines* até a implementação de infraestrutura em nuvem.

Neste ponto, você já conhece os conceitos e já desenvolveu habilidades técnicas em ferramentas de orquestração e plataformas de dados como **Databricks**.

Agora, desejamos incrementar sua capacidade de **projetar sistemas** de forma estruturada e comunicar suas decisões de **arquitetura** de maneira clara e fundamentada.

!!! quote "Engenheiro de Dados Sênior"
    *"Dominar ferramentas é importante, mas algo que diferencia um engenheiro júnior de um pleno ou sênior é a capacidade de enxergar o sistema como um todo, entender os trade-offs de cada decisão de arquitetura e comunicar isso de forma clara para diferentes audiências."*

Esta será uma habilidade importante em processo seletivos que tenham uma etapa de **entrevistas de system design** (*design* de sistemas).

## System Design Interviews?

Uma **entrevista de system design** é um tipo de entrevista técnica onde o candidato precisa projetar a arquitetura de um sistema de *software* em larga escala.

Diferentemente de questões de algoritmos, **SQL** ou estruturas de dados, que geralmente têm respostas específicas, as questões de *system design* são **deliberadamente vagas e abertas**.

!!! example "Exemplos de questões:"
    - *"Projete um sistema de feed de notícias como o do Facebook."*
    - *"Como você construiria um sistema de contador de cliques?"*
    - *"Projete uma plataforma de streaming de vídeo como o YouTube."*
    - *"Desenhe a arquitetura de um data warehouse para análise de bilhões de eventos de usuários."*

Algumas questões das *interviews* que realizamos já possuem questões parecidas. Nosso objetivo é explorar essas questões de forma mais sistêmica, entendendo como estruturar a resposta, quais aspectos considerar e como comunicar suas decisões.

## Por que?

A adoção de entrevistas de *system design* ocorre porque elas avaliam habilidades importantes de um engenheiro de dados ou de *software*.

Durante uma entrevista de *system design*, o entrevistador está observando como o candidato:

- **Analisa problemas vagos e complexos**: A capacidade de pegar um problema mal definido e estruturá-lo de forma clara é essencial. No mundo real, requisitos raramente chegam perfeitamente especificados. Um engenheiro precisa saber fazer as perguntas certas para entender o escopo real do problema.

- **Decompõe sistemas complexos**: Sistemas de larga escala são compostos por múltiplos componentes que interagem entre si. A habilidade de quebrar um problema grande em partes menores e gerenciáveis é fundamental para construir soluções escaláveis e manuteníveis.

- **Comunica ideias técnicas**: Engenharia não é um trabalho solitário. A capacidade de explicar decisões arquiteturais, discutir alternativas e justificar escolhas para diferentes audiências (outros engenheiros, gerentes de produto, executivos) é importante para o sucesso de qualquer projeto.

- **Identifica e avalia trade-offs**: Toda decisão de arquitetura envolve compromissos. Usar *cache* melhora performance mas aumenta complexidade. Normalizar dados reduz redundância mas pode prejudicar performance de leitura. Um engenheiro experiente reconhece esses *trade-offs* e faz escolhas conscientes **baseadas nos requisitos** do sistema.

- **Considera restrições e requisitos**: Soluções desenvolvidas precisam atender requisitos de performance, escalabilidade, disponibilidade, custo e segurança. É importante identificar e priorizar esses requisitos.

!!! info "Similaridade com o trabalho real"
    Projetar um novo *pipeline* de dados, migrar um sistema legado ou otimizar uma arquitetura existente envolvem os mesmos processos de análise, decomposição e avaliação de alternativas.

## Preparação

A preparação para entrevistas de *system design* não é apenas sobre passar em processos seletivos. O conhecimento e as habilidades desenvolvidas neste processo têm valor duradouro para sua carreira como engenheiro de dados.

Nas próximas seções, vamos explorar um *framework* sistemático para abordar questões de *system design*!
