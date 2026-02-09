# Apache Iceberg

## Introdução

O **Apache Iceberg** é uma tecnologia de gerenciamento de tabelas de código aberto, que surgiu como uma das principais opções para implementar a camada de software de armazenamento transacional em arquiteturas **Data Lakehouse**. 

Desenvolvido inicialmente pela **Netflix** e posteriormente doado para a **Apache Software Foundation**, o **Iceberg** é uma alternativa ao **Delta Lake** e **Apache Hudi**, oferecendo características muito semelhantes para aprimorar as funcionalidades de um **data lake** tradicional.

## Principais Características

As principais características e funcionalidades do **Apache Iceberg** incluem:

- **Tecnologia de Gerenciamento de Tabelas**: O **Iceberg** é, fundamentalmente, uma tecnologia que gerencia tabelas, assim como o **Apache Hudi**, proporcionando uma interface consistente para operações de dados.

- **Camada de Armazenamento Transacional**: Ele atua como uma camada de software transacional que executa sobre um **data lake** existente, adicionando recursos semelhantes aos de um banco de dados relacional (RDW - Relational Data Warehouse), o que melhora significativamente a confiabilidade, segurança e desempenho do **data lake**.

- **Rastreamento de Arquivos**: O **Iceberg** pode rastrear todos os arquivos que compõem uma tabela, mantendo um controle preciso sobre a estrutura e organização dos dados.

- **Viagem no Tempo (Time Travel)**: Uma das funcionalidades mais poderosas do **Iceberg** é sua capacidade de rastrear arquivos em cada "snapshot" (instantâneo) da tabela ao longo do tempo, permitindo a funcionalidade de **"viagem no tempo"** (time travel) em um ambiente de **data lake**. Isso possibilita consultar dados em estados anteriores e recuperar versões específicas.

- **Evolução de Esquema**: Suporta a evolução de esquema de forma seamless, o que significa que o esquema dos dados pode ser alterado ao longo do tempo sem quebrar consultas existentes, proporcionando flexibilidade para mudanças nos requisitos de negócio.

- **Escalabilidade**: Projetado para gerenciar tabelas em escala de **petabytes**, atendendo às demandas de grandes volumes de dados empresariais.

- **Serialização Híbrida**: É um exemplo de tecnologia de serialização híbrida, que combina múltiplas técnicas de serialização ou integra a serialização com camadas de abstração adicionais, como o gerenciamento de esquema, otimizando o desempenho e a eficiência.

Em suma, o **Apache Iceberg** é uma solução essencial para transformar um **data lake** tradicional em um **Data Lakehouse** robusto, conferindo-lhe recursos de gerenciamento e confiabilidade que antes eram exclusivos dos **data warehouses** relacionais.

Com o **Iceberg**, organizações podem:
- Manter a flexibilidade e economia de um **data lake**
- Obter a confiabilidade e performance de um **data warehouse**
- Implementar operações **ACID** em ambientes distribuídos
- Facilitar a governança e auditoria de dados

!!! tip "Leitura recomendada"
    [Why did Databricks Acquire Tabular](https://www.dqlabs.ai/blog/why-did-databricks-acquire-tabular/)

Vamos praticar com o Apache Iceberg.

## Preparar ambiente

!!! exercise
    Crie uma pasta `10-data-lakehouse/02-iceberg` em seu diretório de trabalho e navegue até ela:

    <div class="termy">

    ```
    $ mkdir -p 10-data-lakehouse/02-iceberg
    $ cd 10-data-lakehouse/02-iceberg
    ```

    </div>

## Docker compose

Para esta seção da aula, o arquivo `docker-compose.yml` deve conter:

```yaml { .copy }
services:
  spark-iceberg:
    image: tabulario/spark-iceberg
    container_name: spark-iceberg
    build: spark/
    networks:
      iceberg_net:
    depends_on:
      - rest
      - minio
    volumes:
      - ./warehouse:/home/iceberg/warehouse
      - ./notebooks:/home/iceberg/notebooks/notebooks
    environment:
      - AWS_ACCESS_KEY_ID=admin
      - AWS_SECRET_ACCESS_KEY=password
      - AWS_REGION=us-east-1
    ports:
      - 8888:8888
      - 8080:8080
      - 10000:10000
      - 10001:10001
  rest:
    image: apache/iceberg-rest-fixture
    container_name: iceberg-rest
    networks:
      iceberg_net:
    ports:
      - 8181:8181
    environment:
      - AWS_ACCESS_KEY_ID=admin
      - AWS_SECRET_ACCESS_KEY=password
      - AWS_REGION=us-east-1
      - CATALOG_WAREHOUSE=s3://warehouse/
      - CATALOG_IO__IMPL=org.apache.iceberg.aws.s3.S3FileIO
      - CATALOG_S3_ENDPOINT=http://minio:9000
  minio:
    image: minio/minio
    container_name: minio
    environment:
      - MINIO_ROOT_USER=admin
      - MINIO_ROOT_PASSWORD=password
      - MINIO_DOMAIN=minio
    networks:
      iceberg_net:
        aliases:
          - warehouse.minio
    ports:
      - 9001:9001
      - 9000:9000
    command: ["server", "/data", "--console-address", ":9001"]
  mc:
    depends_on:
      - minio
    image: minio/mc
    container_name: mc
    networks:
      iceberg_net:
    environment:
      - AWS_ACCESS_KEY_ID=admin
      - AWS_SECRET_ACCESS_KEY=password
      - AWS_REGION=us-east-1
    entrypoint: |
      /bin/sh -c "
      until (/usr/bin/mc alias set minio http://minio:9000 admin password) do echo '...waiting...' && sleep 1; done;
      /usr/bin/mc rm -r --force minio/warehouse;
      /usr/bin/mc mb minio/warehouse;
      /usr/bin/mc policy set public minio/warehouse;
      tail -f /dev/null
      "
networks:
  iceberg_net:
```

!!! exercise
    Dê uma lida com atenção no arquivo `docker-compose.yml`.

    Chame o professor se não entender alguma coisa.

!!! exercise text long
    Quantos serviços estão sendo inicializados com este `docker-compose.yml`? Quais são eles e qual a função de cada um?

    !!! answer
        Quatro serviços estão sendo inicializados:

        1. **spark-iceberg**: Este serviço executa o Apache Spark com suporte ao Apache Iceberg, permitindo a criação e manipulação de tabelas Iceberg.
        2. **rest**: Este serviço é um fixture REST para o Apache Iceberg, que fornece uma API REST para interagir com o catálogo Iceberg.
        3. **minio**: Este serviço executa o MinIO, um armazenamento de objetos compatível com S3, que serve como o backend de armazenamento para os dados do Iceberg.
        4. **mc**: Este serviço executa o cliente MinIO (mc) para configurar o bucket necessário no MinIO e garantir que o ambiente esteja pronto para uso.

        Esses serviços juntos criam um ambiente completo para trabalhar com tabelas Iceberg em um data lakehouse.

!!! exercise
    Crie um arquivo `docker-compose.yml` com o conteúdo acima e inicialize os serviços:
    
    <div class="termy">

    ```
    $ docker compose up
    ```

    </div>

    Aguarde uns instantes até que os serviços estejam totalmente inicializados.

!!! exercise text short
    Acesse o serviço do **MinIO**. Existe algum bucket já criado? Como ele foi criado?

    !!! info "Info!"
        O serviço **MinIO** está disponível na URL [http://localhost:9001](http://localhost:9001) em seu navegador.

    !!! answer
        Sim, existe um bucket `warehouse` já criado. Ele foi criado automaticamente pelo serviço **mc** na primeira vez que foi executado.

## Criar tabelas

Vamos utilizar o **PyIceberg** para criar e manipular tabelas no Iceberg.

!!! exercise
    A imagem **Docker** que estamos utilizando já contém alguns notebooks de exemplo.

    Acesse o [Jupyter Notebook Getting Started](http://localhost:8888/notebooks/PyIceberg%20-%20Getting%20Started.ipynb).

!!! exercise
    Leia o notebook com atenção e execute os códigos até antes de iniciar a seção **DuckDB**.

!!! exercise text long
    Ao terminar a execução do notebook, confira no serviço **MinIO** se os arquivos da tabela foram criados.

    Acesse `warehouse/default/taxis` e veja os arquivos. Qual a função das pastas `data` e `metadata`?

    !!! answer
        A pasta `data` contém os arquivos de dados reais da tabela, enquanto a pasta `metadata` contém os arquivos de metadados que descrevem a estrutura da tabela, incluindo informações sobre partições, esquema e snapshots.

!!! exercise
    Acesse o [Jupyter Notebook PyIceberg - Write support](http://localhost:8888/notebooks/PyIceberg%20-%20Write%20support.ipynb).

    Execute os códigos do notebook. Se tiver dúvidas, chame o professor.

!!! exercise
    Acesse o [Jupyter Notebook Iceberg - View Support](http://localhost:8888/notebooks/Iceberg%20-%20View%20Support.ipynb).

    Execute os códigos do notebook. Se tiver dúvidas, chame o professor.

Acesse o servidor **Jupyter Notebook** no endereço [http://localhost:8888](http://localhost:8888). Você irá encontrar vários notebooks de exemplo para explorar o **Iceberg**!

Na próxima seção, iremos utilizar o **Trino** para consultar as tabelas que criamos utilizando o formato **Iceberg**.